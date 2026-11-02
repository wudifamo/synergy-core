# Deskflow 长期记忆

## 剪贴板大小限制
- GUI「限制为 N MB」存在 `server/clipboardSize`，默认 3MB。
- 服务端通过 `kOptionClipboardSharingSize` 下发 KB 值。
- 客户端接收原先只用本地默认 3MB（`m_maximumClipboardReceiveSize`），不跟服务器 300MB 走。现有 release 的变通：客户端机器也要进一次「服务器配置」把限制改成 300。2026-08-24 源码已改为收到 CLSZ 后同步接收上限。
- 桌面模式 core 进程需传 `--settings`，否则可能读不到 GUI 里改过的值。
- 现有 release：剪贴板超限会 `requestDisconnect` 直接断连。源码已改为忽略超限剪贴板、保持连接。
