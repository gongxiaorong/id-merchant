# index.html 多语言方案 Spec（外置 JSON 语言包）

## Why

当前 `index.html` 是一个单文件 Vue 3 原型应用（约 277KB），全站文案均为硬编码中文（约 4948 处含中文的行）。虽然已有 `appLang` 状态和 4 种语言选项（简体中文 / 繁體中文（中國香港）/ English / Bahasa Indonesia），但切换语言后 **界面文案不会变化**——`appLang` 仅作为标签展示，未接入任何翻译字典。需要建立一套完整的多语言（i18n）方案，使所有用户可见文案能根据 `appLang` 动态切换。

本方案采用 **外置 JSON 语言包** 方式，将翻译条目从 `index.html` 中分离为独立的 `.json` 文件，便于维护、翻译协作和按需加载。

## What Changes

- 新建 `locales/` 目录，包含 4 个外置 JSON 语言包文件：`zh-CN.json`、`zh-HK.json`、`en.json`、`id.json`
- 在 `index.html` 的 `<script>` 中实现 `t(key, params)` 翻译函数，从已加载的语言包中取值，支持占位符插值（如 `{count}`、`{name}`）
- 实现 `loadLocale(lang)` 异步加载函数，通过 `fetch()` 按需加载对应语言的 JSON 文件，加载完成后存入响应式 `messages` 对象
- 页面启动时先加载 `zh-CN` 语言包作为默认/基础语言，再根据 `appLang` 加载当前语言
- 修改 `selectLang` / `selectLangFromLogin` 函数：切换语言时调用 `loadLocale(id)` 加载新语言包，加载完成后触发界面响应式更新
- 将模板中所有硬编码中文文案替换为 `{{ t('key') }}` 或 `:placeholder="t('key')"` 形式
- 将 JS 逻辑中的硬编码文案（`toast('已退出登录','info')` 等）替换为 `toast(t('logout.success'),'info')` 形式
- 将 `permGroups` 等数据结构中的中文 `name` / `n` 字段改为 i18n key
- `<html lang="zh-CN">` 改为动态绑定 `:lang="appLang"`
- 语言包加载期间显示加载状态（如骨架屏或 loading），避免空白闪烁
- 保持现有 UI 布局、交互逻辑、样式完全不变

## Impact

- Affected code: `index.html`（HTML 模板 + CSS + Vue JS 逻辑）+ 新建 `locales/` 目录（4 个 JSON 文件）
- 影响范围：4 个 Tab（首页 / 车辆 / 订单 / 我的）+ 登录流程 + 告警流程 + 消息中心 + 版本检测弹窗 + Demo 调试面板 + 权限字典
- 预计翻译条目：300-500 个 key
- **BREAKING**：`index.html` 不再自包含，依赖同目录下 `locales/` 文件夹中的 JSON 语言包；需通过 HTTP 服务器访问（`fetch()` 不支持 `file://` 协议）

## ADDED Requirements

### Requirement: 外置 JSON 语言包文件

系统 SHALL 在 `index.html` 同级目录下创建 `locales/` 文件夹，包含 `zh-CN.json`、`zh-HK.json`、`en.json`、`id.json` 四个 JSON 文件。每个文件为一个扁平或嵌套的 key-value 对象，按模块组织。

#### Scenario: 文件结构

- **WHEN** 开发者查看 `locales/` 目录
- **THEN** 应看到 4 个 JSON 文件，分别对应 4 种语言
- **AND** 每个文件内部按模块组织，如 `{"tab": {"home": "首页", ...}, "login": {...}, ...}`

#### Scenario: JSON 格式

- **WHEN** 打开 `locales/en.json`
- **THEN** 内容为有效的 JSON 对象
- **AND** key 命名使用点分路径的嵌套对象（如 `{"tab": {"home": "Home"}}`）
- **AND** 支持占位符语法 `{var}`（如 `"logout_success": "{name} has logged out"`）

### Requirement: loadLocale() 异步加载函数

系统 SHALL 提供 `loadLocale(lang)` 异步函数，通过 `fetch('locales/' + lang + '.json')` 加载对应语言包。

#### Scenario: 首次加载

- **WHEN** 页面初始化时
- **THEN** SHALL 先加载 `zh-CN` 语言包作为 fallback 基础
- **AND** 然后加载 `appLang` 对应的语言包
- **AND** 两次加载完成后初始化 Vue 应用

#### Scenario: 切换语言时加载

- **WHEN** 用户切换语言到 `en`
- **THEN** SHALL 调用 `loadLocale('en')` 加载 `locales/en.json`
- **AND** 加载成功后将翻译条目存入响应式 `messages` 对象
- **AND** 触发界面即时更新

#### Scenario: 加载失败处理

- **WHEN** `fetch` 请求失败（网络错误或文件不存在）
- **THEN** SHALL 保持当前语言不变
- **AND** 显示 toast 提示「语言包加载失败」
- **AND** fallback 到已加载的 `zh-CN`

#### Scenario: 缓存已加载语言包

- **WHEN** 用户切换到一个已加载过的语言
- **THEN** SHALL 直接使用缓存的语言包数据，不重复 `fetch`

### Requirement: t() 翻译函数

系统 SHALL 提供一个 `t(key, params)` 函数，接收点分路径 key（如 `'home.title'`）和可选的插值参数对象。

#### Scenario: 基本翻译

- **WHEN** `appLang` 为 `'en'`，调用 `t('tab.home')`
- **THEN** 返回 `'Home'`

#### Scenario: 占位符插值

- **WHEN** `appLang` 为 `'zh-CN'`，调用 `t('toast.logout', { name: '王建国' })`
- **THEN** 返回 `'王建国 已退出登录'`（若模板为 `'{name} 已退出登录'`）

#### Scenario: Fallback 机制

- **WHEN** 当前语言的字典中缺少某个 key
- **THEN** 系统 SHALL 回退到 `zh-CN` 对应的值
- **AND** 若 `zh-CN` 也缺失，返回 key 本身

#### Scenario: 响应式更新

- **WHEN** `loadLocale` 完成并更新 `messages` 后
- **THEN** 所有使用 `t()` 的界面文案 SHALL 即时更新为新语言

### Requirement: 模板文案国际化

所有用户可见的硬编码文案 SHALL 替换为 `t()` 调用，包括但不限于：

#### Scenario: 文本内容

- **WHEN** 模板中有 `<span>首页</span>`
- **THEN** 替换为 `<span>{{ t('tab.home') }}</span>`

#### Scenario: 属性文案

- **WHEN** 模板中有 `placeholder="搜索国家/地区或区号"`
- **THEN** 替换为 `:placeholder="t('dialcode.searchPlaceholder')"`

#### Scenario: 动态文案

- **WHEN** JS 中有 `toast('登录成功','success')`
- **THEN** 替换为 `toast(t('toast.login.success'),'success')`

### Requirement: 语言切换响应式

`appLang` 和 `messages` 作为 Vue 响应式数据，其值变化时 SHALL 触发所有依赖 `t()` 的模板和计算属性重新渲染。

#### Scenario: 切换语言后界面更新

- **WHEN** 用户在「我的 → 切换语言」中选择 English
- **THEN** 系统加载 `locales/en.json`
- **AND** 加载完成后底部 Tab、页面标题、按钮文案等全部即时变为英文
- **AND** 不需要刷新页面

#### Scenario: 登录页切换语言

- **WHEN** 用户在登录页点击语言芯片选择 Bahasa Indonesia
- **THEN** 系统加载 `locales/id.json`
- **AND** 加载完成后登录页所有文案变为印尼语
- **AND** 登录后主界面也保持印尼语

### Requirement: 语言包加载状态

#### Scenario: 加载中状态

- **WHEN** 语言包正在加载（`fetch` 进行中）
- **THEN** 切换语言的操作 SHALL 防抖（禁止重复点击）
- **AND** 可选展示轻量 loading 指示器

#### Scenario: html lang 属性同步

- **WHEN** `appLang` 变化为 `'en'`
- **THEN** `<html>` 标签的 `lang` 属性 SHALL 变为 `en`

## MODIFIED Requirements

### Requirement: selectLang / selectLangFromLogin

现有 `selectLang(id)` 仅设置 `appLang.value`。修改后 SHALL：
1. 调用 `loadLocale(id)` 异步加载语言包
2. 加载成功后设置 `appLang.value = id`
3. 关闭语言选择面板
4. 若加载失败则保持原语言不变

### Requirement: 权限字典国际化

`permGroups` 数组中的 `name` 和 `n` 字段当前为硬编码中文。修改为使用 i18n key，通过 `t()` 在渲染时翻译。

### Requirement: demo-ops 调试面板国际化

Demo 调试面板（`.demo-ops`）中的标签和权限名称 SHALL 也支持多语言切换。

## REMOVED Requirements

无。所有现有功能保持不变，仅增加国际化能力。
