# Checklist

- [x] `<title>` 标签初始值不再硬编码中文，非中文语言下不会出现中文标题闪烁
- [x] `document.title` 在语言切换后正确更新为当前语言的翻译
- [x] 账号详情页 demo 姓名 `小迪` 已替换为中性英文名，在任意语言下合理展示
- [x] 所有 toast 调用已使用 `t()` 包裹（验证通过：无硬编码中文 toast）
- [x] 告警类型枚举值已通过 `alertTypeLabel()` 正确翻译
- [x] 车辆状态枚举值已通过 `vehStatusLabel()` 正确翻译
- [x] 忽略原因枚举值已通过 `ignoreReasonLabel()` 正确翻译
- [x] demo-ops 面板所有文案保持中文，不参与语言切换
- [x] 语言名称标签（`langOptions`）保持原生形式，不翻译
- [x] 车型名称、车牌号、地点等 demo 数据作为专有名词，不翻译