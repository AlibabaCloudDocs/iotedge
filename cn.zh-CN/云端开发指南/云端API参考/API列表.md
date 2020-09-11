---
keyword: [物联网, Link IoT Edge, 物联网边缘计算, 云端, API]
---

# API列表

以下是物联网边缘计算API列表。

## 实例管理API

|API|描述|
|:--|:-|
|[CreateEdgeInstance]()|创建边缘实例。|
|[DeleteEdgeInstance]()|删除边缘实例。|
|[UpdateEdgeInstance]()|更新边缘实例。|
|[GetEdgeInstance]()|获取边缘实例详情。|
|[QueryEdgeInstance]()|查询当前账号下的所有边缘实例。|

## 驱动管理API

|API|描述|
|:--|:-|
|[CreateEdgeDriver]()|创建驱动。|
|[DeleteEdgeDriver]()|删除已创建的驱动。|
|[BatchGetEdgeDriver]()|批量查询驱动信息。|
|[QueryEdgeDriver]()|分页查询驱动信息。|
|[CreateEdgeDriverVersion]()|新增驱动版本。|
|[DeleteEdgeDriverVersion]()|删除驱动的某一版本。|
|[UpdateEdgeDriverVersion]()|更新驱动版本。|
|[GetEdgeDriverVersion]()|查询驱动某一版本的信息。|
|[ReleaseEdgeDriverVersion]()|发布驱动的某一版本。|
|[QueryEdgeDriverVersion]()|分页查询驱动版本列表。|
|[CreateEdgeOssPreSignedAddress]()|创建对象存储（OSS）预签名地址。|

## 场景联动API

|API|描述|
|:--|:-|
|[CreateSceneRule]()|创建场景联动规则。|
|[DeleteSceneRule]()|删除场景联动规则。|
|[UpdateSceneRule]()|更新场景联动规则。|
|[GetSceneRule]()|获取场景联动规则详情。|
|[QuerySceneRule]()|查询场景联动规则列表。|
|[EnableSceneRule]()|启动场景联动规则。|
|[DisableSceneRule]()|停止场景联动规则。|
|[TriggerSceneRule]()|触发场景联动规则。|
|[QuerySummarySceneRuleLog]()|查询场景联动规则日志。|
|[QueryDetailSceneRuleLog]()|查看场景联动规则日志的详细信息。|

## 实例网关管理API

|API|描述|
|:--|:-|
|[BindGatewayToEdgeInstance]()|分配网关到边缘实例中。|
|[QueryEdgeInstanceGateway]()|查询边缘实例中的网关。|
|[ReplaceEdgeInstanceGateway]()|替换已绑定到边缘实例的网关。|

## 实例驱动管理API

|API|描述|
|:--|:-|
|[BindDriverToEdgeInstance]()|分配驱动到边缘实例中。|
|[UnbindDriverFromEdgeInstance]()|从边缘实例中移除驱动。|
|[QueryEdgeInstanceDriver]()|查询边缘实例的驱动列表。|
|[SetEdgeInstanceDriverConfigs]()|配置边缘实例驱动。|
|[ClearEdgeInstanceDriverConfigs]()|清空边缘实例的驱动配置。|
|[BatchGetEdgeInstanceDriverConfigs]()|批量获取边缘实例的驱动配置。|

## 实例设备管理API

|API|描述|
|:--|:-|
|[BatchBindDeviceToEdgeInstanceWithDriver]()|批量分配设备到边缘实例中，并为设备设置驱动。|
|[BatchUnbindDeviceFromEdgeInstance]()|批量移除边缘实例中的设备。|
|[QueryEdgeInstanceDevice]()|查询边缘实例中的设备列表。|
|[BatchGetDeviceBindStatus]()|批量获取网关或设备绑定到边缘实例的状态。|
|[BatchSetEdgeInstanceDeviceConfig]()|批量配置边缘实例中的设备。|
|[BatchClearEdgeInstanceDeviceConfig]()|批量清空边缘实例中设备的配置。|
|[BatchGetEdgeInstanceDeviceConfig]()|批量获取边缘实例中设备的配置。|
|[QueryEdgeInstanceDeviceByDriver]()|查询驱动下关联的子设备。|
|[BatchGetEdgeInstanceDeviceDriver]()|批量获取子设备关联的驱动。|
|[BatchSetEdgeInstanceDeviceChannel]()|批量关联驱动通道到子设备。|
|[BatchGetEdgeInstanceDeviceChannel]()|批量获取子设备关联的驱动通道。|

## 实例场景联动API

|API|描述|
|---|--|
|[BindSceneRuleToEdgeInstance]()|绑定场景联动规则到边缘实例。|
|[UnbindSceneRuleFromEdgeInstance]()|从边缘实例中移除场景联动规则。|
|[QueryEdgeInstanceSceneRule]()|分页查询边缘实例中的场景联动规则列表。|

## 实例通道管理API

|API|描述|
|---|--|
|[CreateEdgeInstanceChannel]()|创建边缘实例中的驱动通道。|
|[BatchDeleteEdgeInstanceChannel]()|批量删除边缘实例中驱动的通道。|
|[UpdateEdgeInstanceChannel]()|更新边缘实例中的驱动通道。|
|[BatchGetEdgeInstanceChannel]()|批量查询边缘实例中的驱动通道。|
|[QueryEdgeInstanceChannel]()|查询边缘实例中的驱动通道列表。|

## 实例应用管理API

|API|描述|
|---|--|
|[BindApplicationToEdgeInstance]()|绑定边缘应用到边缘实例。|
|[UnbindApplicationFromEdgeInstance]()|从边缘实例中移除边缘应用。|

## 实例角色管理API

|API|描述|
|---|--|
|[BindRoleToEdgeInstance]()|绑定角色到边缘实例。|
|[UnbindRoleFromEdgeInstance]()|解除边缘实例中已绑定的角色。|

## 实例部署API

|API|描述|
|:--|:-|
|[CreateEdgeInstanceDeployment]()|创建边缘实例部署单。|
|[CloseEdgeInstanceDeployment]()|关闭边缘实例部署单。|
|[GetEdgeInstanceDeployment]()|获取边缘实例部署单详情。|
|[QueryEdgeInstanceHistoricDeployment]()|查询边缘实例历史部署单记录。|

物联网平台的云端API调用说明，请访问[API列表](/cn.zh-CN/云端开发指南/云端API参考/API列表.md)。

