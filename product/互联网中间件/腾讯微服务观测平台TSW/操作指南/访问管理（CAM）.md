## 操作场景
您可以通过使用访问管理（Cloud Access Management，CAM）策略让用户拥有在腾讯微服务观测平台 TSW（Tencent Service Watcher，TSW）控制台中查看和使用特定资源的权限。本文档提供了查看和使用资源的权限示例，指导用户如何使用控制台的特定部分的策略。

## 操作示例
### TSW 的全读写策略
如果您希望用户拥有创建和管理 TSW 环境的权限，您可以对该用户使用名称为：QcloudTSWFullAccess 的策略。该策略是通过让用户对 TSW 中所有资源都具有操作的权限来达到目的。
具体操作步骤如下：
参考 [授权管理](https://cloud.tencent.com/document/product/598/10602)，将预设策略 QcloudTSWFullAccess 授权给用户。

### TSW 的只读策略
如果您希望用户拥有查看 TSW 环境以及环境中服务运行状态的权限，但是不具有创建、删除、修改环境配置与服务配置的权限，您可以对该用户使用名称为：QcloudTSWReadOnlyAccess 的策略。该策略是通过让用户分别对如下操作 TSW 中所有以单词 “Describe” 开头的所有操作具有操作的权限来达到目的。具体操作步骤如下：
参考 [授权管理](https://cloud.tencent.com/document/product/598/10602)，将预设策略 QcloudTSWReadOnlyAccess 授权给用户。

### TSW 以及相关资源的全读写策略
如果您希望用户拥有创建和管理 TSW 环境的权限，还希望用户拥有查看环境监控（Monitor）数据与配置、查看服务关联日志（CLS）的权限，您可以复制以下策略。该策略是通过让用户分别对如下操作具有操作权限来达到目的：
- TSW 中的所有操作。
- 日志服务 CLS 中的 listLogset 操作和 listTopic 操作。
- 云监控 Monitor 的 GetMonitorData 操作。

参考 [创建自定义策略](https://cloud.tencent.com/document/product/598/37739)，在策略中手动创建该策略，授予用户。
可复制下方策略模板：
```
{
 "version": "2.0",
 "statement": [
     {
         "action": [
             "name/tsw:*",
             "name/cls:listTopic",
             "name/cls:listLogset",
             "name/monitor:GetMonitorData"
         ],
         "resource": "*",
         "effect": "allow"
     }
  ]
 }
```

>?如果您希望授予用户部分环境的权限，进行更细粒度的授权，您需要将resource中的内容，根据您需要授权的环境进行调整，TSW环境资源的六段式如下：
`qcs::tsw:{地域}:uin/{主账号}:EnvironmentName/{环境名}`
您需要将"resource": "*"中的 * 替换为相应的资源六段式。更多资源描述方式，请参考 [资源描述方式](https://cloud.tencent.com/document/product/598/10606)。

### TSW 以及相关资源的只读策略
如果您希望用户拥有查看 TSW 环境的权限，还希望用户拥有查看环境监控（Monitor）数据与查看服务关联日志（CLS）的权限，您可以复制以下策略。该策略是通过让用户分别对如下操作具有操作权限来达到目的：
- TSW 中的以单词 “Describe” 开头的所有操作。
- 日志服务 CLS 中的 listLogset 操作和 listTopic 操作。
- 云监控 Monitor 的 GetMonitorData 操作。

参考 [创建自定义策略](https://cloud.tencent.com/document/product/598/37739)，在策略中手动创建该策略，授予用户。
可复制下方策略模板：
```
{
 "version": "2.0",
 "statement": [
     {
         "action": [
             "name/tsw:Describe*",
             "name/cls:listTopic",
             "name/cls:listLogset",
             "name/monitor:GetMonitorData"
         ],
         "resource": "*",
         "effect": "allow"
     }
  ]
}
```
>?如果您希望授予用户部分环境的权限，进行更细粒度的授权，您需要将 resource 中的内容，根据您需要授权的环境进行调整，TSW 环境资源的六段式如下：
`qcs::tsw:{地域}:uin/{主账号}:EnvironmentName/{环境名}`
您需要将"resource": "*"中的 * 替换为相应的资源六段式。更多资源描述方式，请参考 [资源描述方式](https://cloud.tencent.com/document/product/598/10606)。

权限与访问管理的更多指引，请参考访问管理文档。推荐您熟悉：
- [权限](https://cloud.tencent.com/document/product/598/10600) 与 [策略](https://cloud.tencent.com/document/product/598/10601) 的定义
- [授权指南](https://cloud.tencent.com/document/product/598/37739) 相关步骤
