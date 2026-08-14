# Tasks

- [ ] Task 1: 设计 i18n 架构与加载机制
  - [ ] SubTask 1.1: 设计翻译字典的模块化 key 命名规范（按页面/功能分组，如 `tab.*`、`login.*`、`home.*`、`vehicles.*`、`orders.*`、`profile.*`、`alert.*`、`toast.*`、`common.*` 等）
  - [ ] SubTask 1.2: 实现 `t(key, params)` 翻译函数，支持点分路径查找、占位符插值 `{var}`、fallback 到 `zh-CN`
  - [ ] SubTask 1.3: 实现 `loadLocale(lang)` 异步加载函数：`fetch('locales/' + lang + '.json')`，加载成功后存入响应式 `messages` 对象，支持缓存已加载语言包
  - [ ] SubTask 1.4: 实现 `messages` 响应式对象结构（`ref({})`），存储已加载的所有语言包数据
  - [ ] SubTask 1.5: 实现 `localeLoading` 响应式状态，标记语言包加载中
  - [ ] SubTask 1.6: 实现 `loadLocale` 失败处理：toast 提示 + 保持原语言 + fallback 到 `zh-CN`
  - [ ] SubTask 1.7: 页面启动流程：先 `loadLocale('zh-CN')` → 再 `loadLocale(appLang)` → 初始化 Vue 应用
  - [ ] SubTask 1.8: 将 `t`、`messages`、`loadLocale`、`localeLoading` 挂载到 Vue setup 返回值
  - [ ] SubTask 1.9: 修改 `<html lang="zh-CN">` 为 Vue 动态绑定

- [ ] Task 2: 创建 `locales/` 目录与 zh-CN.json 基础语言包
  - [ ] SubTask 2.1: 创建 `locales/` 目录及 `zh-CN.json` 文件骨架
  - [ ] SubTask 2.2: 提取登录模块文案（login.*），包括手机号/邮箱/账号登录、验证码、协议同意、语言选择等
  - [ ] SubTask 2.3: 提取底部 Tab 栏文案（tab.*）：首页、车辆、订单、我的
  - [ ] SubTask 2.4: 提取首页模块文案（home.*）：经营数据卡片、车辆运营统计、最近告警、告警中心、消息中心
  - [ ] SubTask 2.5: 提取车辆模块文案（vehicles.*）：列表、详情、地图、轨迹、新增/编辑、筛选、车控操作
  - [ ] SubTask 2.6: 提取订单模块文案（orders.*）：列表、详情、筛选、退款记录、客户资料、操作按钮
  - [ ] SubTask 2.7: 提取我的/设置模块文案（profile.*）：菜单项、设置页、语言切换、账号管理、车型管理、客服信息等
  - [ ] SubTask 2.8: 提取告警模块文案（alert.*）：告警详情、状态标签、操作按钮、忽略弹窗等
  - [ ] SubTask 2.9: 提取通用文案（common.* / toast.*）：toast 消息、确认/取消、空态文案、区号选择等
  - [ ] SubTask 2.10: 提取 Demo 调试面板文案（demo.*）：权限组名、权限项名、调试操作按钮
  - [ ] SubTask 2.11: 提取版本检测弹窗文案（version.*）

- [ ] Task 3: 编写 en.json（English）语言包
  - [ ] SubTask 3.1: 翻译 login.* 模块
  - [ ] SubTask 3.2: 翻译 tab.* 模块
  - [ ] SubTask 3.3: 翻译 home.* 模块
  - [ ] SubTask 3.4: 翻译 vehicles.* 模块
  - [ ] SubTask 3.5: 翻译 orders.* 模块
  - [ ] SubTask 3.6: 翻译 profile.* 模块
  - [ ] SubTask 3.7: 翻译 alert.* 模块
  - [ ] SubTask 3.8: 翻译 common.* / toast.* 模块
  - [ ] SubTask 3.9: 翻译 demo.* 模块
  - [ ] SubTask 3.10: 翻译 version.* 模块

- [ ] Task 4: 编写 zh-HK.json（繁體中文-香港）语言包
  - [ ] SubTask 4.1: 翻译全部模块（可基于 zh-CN 做繁体转换）

- [ ] Task 5: 编写 id.json（Bahasa Indonesia）语言包
  - [ ] SubTask 5.1: 翻译全部模块

- [ ] Task 6: 替换模板中的硬编码文案
  - [ ] SubTask 6.1: 替换登录模块模板文案（login-page 区域，约 L186-L353）
  - [ ] SubTask 6.2: 替换区号选择页文案（dialcode-page 区域，约 L137-L155）
  - [ ] SubTask 6.3: 替换首页模板文案（home tab 区域，约 L358-L570）
  - [ ] SubTask 6.4: 替换车辆模块模板文案（vehicles tab 区域，约 L572-L1062）
  - [ ] SubTask 6.5: 替换订单模块模板文案（orders tab 区域，约 L1063-L1369）
  - [ ] SubTask 6.6: 替换我的/设置模块模板文案（profile tab 区域，约 L1370-L1990）
  - [ ] SubTask 6.7: 替换底部 Tab 栏文案（约 L1992-L2006）
  - [ ] SubTask 6.8: 替换版本检测弹窗文案（约 L2008-L2050）
  - [ ] SubTask 6.9: 替换 Demo 调试面板文案（约 L2051-L2150）

- [ ] Task 7: 替换 JS 逻辑中的硬编码文案
  - [ ] SubTask 7.1: 替换 `toast()` 调用中的硬编码消息（约 41 处）
  - [ ] SubTask 7.2: 替换 `permGroups` 中的 `name` / `n` 字段为 i18n key
  - [ ] SubTask 7.3: 替换 `menuList` 中的 `label` 字段为 i18n key
  - [ ] SubTask 7.4: 替换 `dialCodes` 中的 `name` 字段为 i18n key
  - [ ] SubTask 7.5: 替换 `stores` 中的门店名等硬编码文案
  - [ ] SubTask 7.6: 替换 `demoPagePermCtx` 中的 `title` 等硬编码文案
  - [ ] SubTask 7.7: 替换其他 JS 中零散的硬编码中文（modal 标题、表单验证消息等）
  - [ ] SubTask 7.8: 修改 `selectLang` / `selectLangFromLogin` 函数，调用 `loadLocale` 异步加载

- [ ] Task 8: 验证与回归测试
  - [ ] SubTask 8.1: 通过 HTTP 服务器打开页面，默认 zh-CN 语言下所有文案正确显示
  - [ ] SubTask 8.2: 切换到 English，验证所有页面文案已翻译
  - [ ] SubTask 8.3: 切换到繁體中文，验证所有页面文案已翻译
  - [ ] SubTask 8.4: 切换到 Bahasa Indonesia，验证所有页面文案已翻译
  - [ ] SubTask 8.5: 验证语言切换后无残留中文文案
  - [ ] SubTask 8.6: 验证占位符插值正确工作（如 toast 消息中的变量）
  - [ ] SubTask 8.7: 验证 UI 布局未被破坏（排版无溢出/截断）
  - [ ] SubTask 8.8: 验证语言包加载失败时的 fallback 行为（模拟网络错误）
  - [ ] SubTask 8.9: 验证已加载语言包的缓存机制（切换回已加载语言不重复 fetch）

# Task Dependencies

- Task 2 depends on Task 1（需要 key 命名规范与加载机制）
- Task 3, 4, 5 depend on Task 2（需要 zh-CN.json 作为翻译基准）
- Task 6, 7 depend on Task 1（需要 `t()` 函数可用）
- Task 6, 7 依赖 Task 2（需要 key 已定义）
- Task 8 depends on Task 3, 4, 5, 6, 7（全部替换完成后才能验证）
- Task 3, 4, 5 可并行执行
- Task 6, 7 可并行执行
