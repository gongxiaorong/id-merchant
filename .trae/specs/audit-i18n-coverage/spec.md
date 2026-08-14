# 多语言遗漏检查 Spec

## Why

`index.html` 的多语言方案已基本实现完成（外置 JSON 语言包 + `t()` 翻译函数 + 枚举映射），但需要系统性地审计当前代码中是否还有遗漏的硬编码中文，确保所有用户可见文案都能正确跟随语言切换。

## What Changes

- 审计 `<title>` 标签：初始硬编码中文 `电动车租赁商户管理端 · 首页`，需改为动态设置或使用 i18n key
- 审计账号详情页 demo 数据中的硬编码姓名 `小迪`
- 确认所有 toast 调用已翻译（已验证通过）
- 确认所有枚举值（告警类型、车辆状态、忽略原因）已通过映射函数翻译（已验证通过）
- 确认 demo-ops 面板正确排除在 i18n 之外（已验证通过）
- 确认语言名称标签（`langOptions`）保持不变（语言名应以原生形式展示，不翻译）

## Impact

- Affected specs: `add-i18n-multilingual`
- Affected code: `index.html`（`<title>` 标签、账号详情 demo 数据）
- 影响范围：页面标题初始显示、账号详情页 demo 姓名

## ADDED Requirements

### Requirement: 页面标题动态化

系统 SHALL 确保页面标题 `<title>` 在所有语言下显示正确的翻译文本，而非初始硬编码中文。

#### Scenario: 初始加载
- **WHEN** 页面首次加载（在任何语言包加载之前）
- **THEN** `<title>` 应显示合理的默认值或通过 JS 动态设置
- **AND** 不应在非中文语言下闪现中文标题

#### Scenario: 语言切换后
- **WHEN** 用户切换语言
- **THEN** `document.title` 应更新为当前语言的对应翻译
- **AND** 已通过 `watch(appLang)` 和 `loadLocale()` 中的 `document.title = t('login.title')` 实现

### Requirement: Demo 数据中的姓名处理

系统 SHALL 确保账号详情页中显示的 demo 用户名不因语言切换而产生困惑。

#### Scenario: 非中文语言下显示 demo 姓名
- **WHEN** 当前语言为 English
- **THEN** demo 账号姓名 `小迪` 是否应保持原样（作为专有名词）或替换为中性英文名，需确认

## MODIFIED Requirements

无。

## REMOVED Requirements

无。