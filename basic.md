源仓库：https://github.com/ncatbot/NcatBot 

Issue: https://github.com/ncatbot/NcatBot/issues/36 

PR: https://github.com/ncatbot/NcatBot/pull/37


在整个 QQ 机器人体系里，NapCat 和 SnowLuma 本质上都属于“QQ 客户端适配器（QQ Adapter / Protocol Implementation）”，是“让机器人能够真正连接 QQ”的那一层。

```
机器人业务代码  
↓  
NcatBot（机器人框架）  
↓  
NapCat / SnowLuma（QQ协议适配器）  
↓  
QQ客户端
```
由于 SnowLuma 与 NapCat 的事件字段结构和 API 数据格式存在差异，直接接入 NcatBot 时会导致内部事件模型不兼容，因此需要通过 adapter 层进行字段映射与协议统一，以保证现有 OneBot11/NapCat 生态的向下兼容性。


更具体地说，adapter 层其实做了两件事：

1. 输入方向：把 SnowLuma 的数据 → 转成 NcatBot 认识的数据  
2. 输出方向：把 NcatBot 的 API 调用 → 转成 SnowLuma 能理解的数据  

它本质上是一个“双向协议翻译层”。


