# 系统一览

| 名称           | 编码 | 系统开发方   |
| -------------- | ---- | ------------ |
| 前台服务系统   | FD   | 慧通关       |
| ASN系统        | ASN  | 慧通关       |
| 关务系统       | CMS  | 慧通关       |
| 海关系统数据库 | HGXT | 唯智，慧通关 |
| 电子发票系统   | DZFP | ？           |
| ？             | OWB  | ？           |

# 整体系统架构

![架构图](diagrams/Architecture.png)
[编辑](https://www.draw.io/?title=Architecture.png&url=https%3A%2F%2Fgithub.com%2Fleaderrun-wms%2Fdocs%2Fraw%2Fmaster%2Fdiagrams%2FArchitecture.png%3Ft%3D0)


# 对接接口一览

| 序号 | 接口名称                                 | 发送方 | 接收方 | 服务 | 集成 | 描述                                                                                                                                      |
| ---- | ---------------------------------------- | ------ | ------ | ---- | ---- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| 1    | [入库订单接口](Inbound.md)               | FD     | OWB    |   ok   | OK   | 异步返回处理结果；1.创建会发；2.放行发 OWB 会自动审核往仓库下发；3.关务信息保存可供货代查看                                               |
| 2    | [出库关务接口](Outbound.md)              | OWB    | FD     | OK   |   ok   | 主动推送查询给CMS，CMS实时反馈结果；订单审核发送时，如果反馈结果不成功，WMS可以往下执行；发运之前再次请求，如果反馈结果为不成功，不能发运 |
| 3    | [现金收费](Receivable.md)                | OWB    | FD     |  ok    |      | 创建订单的时候进行计费，提供接口给 CMS 查询，未收的费用项目及金额                                                                         |
| 4    | [现金收费反馈](Payment.md)               | FD     | OWB    |   ok   |      | 实际收费情况反馈，根据费用项目收费时的交易号判断是更新还是新增                                                                            |
| 5    | [库位货品信息](InternalOp.md)            | OWB    | HGXT   |      |      | 收货，上架，移位，下架                                                                                                                    |
| 6    | [改包装关务信息接口](RepackReq.md)       | OWB    | FD     | RFI  |      | 货品包装形态改变，需要重新匹配关务信息                                                                                                    |
| 7    | [改包装关务信息反馈接口](RepackResp.md)  | FD     | OWB    | RFI  |      |                                                                                                                                           |
| 8    | [ASN 信息补录回传](InboundSupp.md)       | OWB    | ASN    | OK   |      | 小程序 asn 信息补录(车型，车牌，CBM，司机姓名，司机电话，预计到仓时间)，记录信息传给 CMS；车辆到仓再传一次                                |
| 9    | [报关单反馈](CustomsFeedbackPDF.md)      | FD     | OWB    |   ok   |      | 根据单号查看报关单（CMS 提供产生的报关单链接）                                                                                            |
| 10   | [单证状态接口](CustomsFeedbackStatus.md) | FD     | OWB    |   ok   |      | 报关等完成后由 CMS 传递给 OWB                                                                                                             |
| 11   | [电子发票接口](ElectronicInvoice.md)     |        |        |      |      |                                                                                                                                           |
| 12   | [仓库信息接口](Warehouse.md)             | FD     | OWB    |   ok   |      |                                                                                                                                           |
| 13   | [客户信息接口](Customer.md)              | FD     | OWB    |   ok   |      |                                                                                                                                           |
| 14   | [订单放行接口](InbaseOderRelease.md)     | FD     | OWB    |   ok   |      |                                                                                                                                           |
| 15   | [出库订单确认申报接口](ConfirmDeclaration.md)     | OWB  | FD    |      |      |  运抵确认出库报关单可申报|

# 环境

## 开发环境

* OWB: TODO
* FD: lhfdbe-test.yunbaoguan.cn:81
* ASN: lhomsbe-test.yunbaoguan.cn:81

## 生产环境
