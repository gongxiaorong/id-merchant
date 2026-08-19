# 枚举字段翻译对照表

> 本文档整理项目中所有**枚举字段**（状态、级别、渠道等固定取值）在四种语言下的翻译，作为统一基准。
>
> 基准语言：**zh-CN（简体中文）**。
>
> 原则：同一中文文案在所有出现位置必须使用同一翻译（尤其枚举值）；本表即唯一权威来源。

- 语言文件路径：`locales/{zh-CN, zh-HK, en, id}.json`
- 键名写法：`模块.键名`（多级用 `.` 连接）

---

## 一、订单状态（orders.status* / orders.quick*）

| zh-CN | zh-HK | en | id | 涉及键名 |
| --- | --- | --- | --- | --- |
| 已创建 | 已建立 | Created | Dibuat | `orders.statusCreated` |
| 待取用 | 待取用 | Awaiting Pickup | Menunggu Pengambilan | `orders.statusPickup`、`orders.quickPending` |
| 进行中 | 進行中 | In Progress | Berlangsung | `orders.statusProgress`、`orders.quickProgress` |
| 待归还 | 待歸還 | Pending Return | Menunggu Pengembalian | `orders.statusReturn`、`orders.quickReturn` |
| 已超期 | 已超期 | Overdue | Terlambat | `orders.statusOverdue`、`orders.quickOverdue` |
| 已完成 | 已完成 | Completed | Selesai | `orders.statusComplete` |
| 已取消 | 已取消 | Cancelled | Dibatalkan | `orders.statusCancelled` |
| 已违约 | 已違約 | Breached | Pelanggaran | `orders.statusBreach` |

## 二、支付状态（orders.pay*）

| zh-CN | zh-HK | en | id | 涉及键名 |
| --- | --- | --- | --- | --- |
| 待支付 | 待支付 | Pending Payment | Menunggu Pembayaran | `orders.payPending` |
| 支付中 | 支付中 | Processing | Pembayaran Diproses | `orders.payProcessing` |
| 已支付 | 已支付 | Paid | Sudah Dibayar | `orders.payPaid` |
| 退款中 | 退款中 | Refunding | Pengembalian Dana Diproses | `orders.payRefunding`、`orders.refundProcessing` |
| 部分退款 | 部分退款 | Partial Refund | Pengembalian Sebagian | `orders.payPartialRefund` |
| 全部退款 | 全部退款 | Full Refund | Pengembalian Penuh | `orders.payFullRefund` |

## 三、告警状态（home.alertFilter* / alert.status*）

| zh-CN | zh-HK | en | id | 涉及键名 |
| --- | --- | --- | --- | --- |
| 全部 | 全部 | All | Semua | `home.alertFilterAll` |
| 待处理 | 待處理 | Pending | Menunggu | `home.alertFilterPending`、`alert.statusPending` |
| 处理中 | 處理中 | Processing | Diproses | `home.alertFilterProcessing`、`alert.statusProcessing` |
| 已忽略 | 已忽略 | Ignored | Diabaikan | `home.alertFilterIgnored`、`alert.statusIgnored`、`alert.timelineIgnored` |
| 已关闭 | 已關閉 | Closed | Ditutup | `home.alertFilterClosed`、`alert.closed`、`alert.statusClosed` |
| 已开始处理 | 已開始處理 | Processing started | Mulai diproses | `alert.startedProcess` |

## 四、告警级别（alert.level*）

| zh-CN | zh-HK | en | id | 涉及键名 |
| --- | --- | --- | --- | --- |
| 高 | 高 | High | Tinggi | `alert.levelHigh` |
| 中 | 中 | Medium | Sedang | `alert.levelMid` |
| 低 | 低 | Low | Rendah | `alert.levelLow` |

## 五、车辆状态（vehicles.status*）

| zh-CN | zh-HK | en | id | 涉及键名 |
| --- | --- | --- | --- | --- |
| 空闲 | 閒置 | Idle | Menganggur | `vehicles.statusIdle` |
| 已锁定 | 已鎖定 | Locked | Terkunci | `vehicles.statusLocked` |
| 占用中 | 佔用中 | Occupied | Terpakai | `vehicles.statusOccupied` |
| 租用中 | 租用中 | Rented | Disewa | `vehicles.statusRented` |
| 已出售 | 已出售 | Sold | Terjual | `vehicles.statusSold` |
| 在线 | 在線 | Online | Online | `vehicles.online`、`vehicles.filterOnline`、`orders.vehicleOnline` |
| 离线 | 離線 | Offline | Offline | `vehicles.offline`、`vehicles.filterOffline` |

## 六、门店级别（profile.storeLevel.*）

| zh-CN | zh-HK | en | id | 涉及键名 |
| --- | --- | --- | --- | --- |
| 代理商门店 | 代理商門店 | Agent Store | Toko Agen | `profile.storeLevel.agent` |
| 运营门店 | 營運門店 | Operated Store | Toko Dikelola | `profile.storeLevel.operated` |

## 七、账号状态（profile.status*）

| zh-CN | zh-HK | en | id | 涉及键名 |
| --- | --- | --- | --- | --- |
| 启用 | 啟用 | Enabled | Aktif | `profile.statusEnabled` |
| 禁用 | 停用 | Disabled | Nonaktif | `profile.statusDisabled` |

## 八、车辆运营统计（home.vehStats.*）

| zh-CN | zh-HK | en | id | 涉及键名 |
| --- | --- | --- | --- | --- |
| 在线车辆 | 在線車輛 | Online Vehicles | Kendaraan Online | `home.vehStats.online` |
| 离线车辆 | 離線車輛 | Offline Vehicles | Kendaraan Offline | `home.vehStats.offline` |

---

## 附：一致性修订记录

| 日期 | 键名 | 变更 |
| --- | --- | --- |
| 2026-08-19 | `orders.refundProcessing` | en：Refund processing → **Refunding**；id：Pengembalian dana diproses → **Pengembalian Dana Diproses**（对齐 `payRefunding`） |
| 2026-08-19 | `orders.searchPhone` | en：Phone number → **Phone Number**；id：Nomor ponsel → **Nomor Ponsel**（统一大小写，非枚举） |
| 2026-08-19 | `login.phoneLabel` | en：Phone → **Phone Number**（统一大小写，非枚举） |
| 2026-08-19 | `orders.reportLost` | en：Report Lost → **Report Vehicle Lost**；id：Laporkan Hilang → **Laporkan Kendaraan Hilang**（对齐 `confirmLostTitle`、`vehicles.confirmLost`） |
