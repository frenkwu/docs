# 改包装关务信息反馈接口

接口定义方：慧通关

## 功能描述

* 货物包装改动完成，关务匹配关系完成后，会产生一个回调
* 在启动变更请求时就需要配置回调接口，否则回调不会产生
* 安全考虑：回调接口路径的设计，可以引入一个状态值来保证回调是出自慧通关系统，按每一票的生成此状态值，让回调的有效性作出验证

## 接口详情

路径：

```
    变更请求的 CallbackUrl 值
```

请求方法：POST

请求内容：

```json
{
    "wmsOrderId": "仓库系统出库订单唯一标识",
    "processId": "OMS的流程ID",
    "success": true, // or false
    "message": "若success为false时的错误信息"
}
```

返回内容：回调处理程序的返回HTTP状态必须是200，否则系统认为回调失败


说明：

* 在回调失败的情况，系统会进行重试
    * 每5分钟一次
    * 一直重试24小时
* 若回调处理接口一直失败，超过了回调的重试范围，则 FD 系统会标记此货物异常


