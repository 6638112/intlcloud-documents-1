当您的账号发生欠费时，系统将为您推送欠费提醒，请在收到欠费通知后，及时前往控制台 [充值中心](https://console.cloud.tencent.com/account/recharge) 进行充值，以免影响您的业务。下面将为您介绍欠费的相关说明。

## 欠费原因

您可以查看以下常见问题，了解欠费原因：

- [享受免费额度为何仍会欠费（扣费）？](https://intl.cloud.tencent.com/document/product/436/10373)



>?
>- 若您对欠费有疑问，可在控制台 [费用账单](https://console.cloud.tencent.com/expense/bill/overview) 页面查阅和核对您的消费明细，操作方式请参见 [查询消费明细](https://intl.cloud.tencent.com/document/product/436/31631) 文档。
>- 若您对具体的扣费项有疑问，可以参见 [计费项](https://intl.cloud.tencent.com/document/product/436/33776) 了解具体的计费项含义及计费规则。
>- 若您想了解各费用的计费和结算周期，请参见 [计费周期](https://intl.cloud.tencent.com/document/product/436/16871)。


## 欠费后的服务状态


1. 账号欠费起24小时内，COS 服务还可正常使用，但在控制台上会有即将停服提醒。您需要在此期间及时充值使账号余额大于等于0，以免影响业务运行。
2. 账号欠费24小时后，COS 服务将自动停止运行，COS 数据将无法读写，而**您的数据所占用的存储空间会持续计费**，欠费金额会累计，直到销毁数据。鉴于数据的重要性，您的数据可以继续保留120天。此时控制台仅提供充值操作，用户续费使账号余额大于等于0后，服务会自动开启。
3. 账号持续欠费120天后，将视为您主动放弃 COS 服务，腾讯云不承诺继续保留您的数据，您的数据将会被销毁，且不可恢复。


## 如何避免和处理欠费？


1. 对于存储在 COS 的数据若您不再使用，您可选择进行删除，以免继续扣费。
2. 您可以在**控制台**>**费用中心**设置**费用预警**功能，当可用余额低于预警阈值时，将向您发送预警通知，详情请参见 [余额预警指引](https://intl.cloud.tencent.com/document/product/555/9942)。
3. 当产生欠费后，请您及时充值使账号余额大于等于0。



## 如何关闭 COS 或停止计费？

COS 暂不支持一键关闭，您可以通过以下方式来实现关闭 COS 或停止计费。

1. 若您不再使用 COS 服务，您可以将 COS 中的所有数据（包括未完成上传的文件碎片、历史版本对象等）完全删除以避免继续计费，无需注销账号（如有使用其他腾讯云服务，注销账号会受到影响）。关于删除数据的步骤说明，请参见如下 [操作指引](#close)。
2. 若您长时间（超过一个月）不使用 COS 服务，可以设置生命周期规则把存储桶中标准存储类型的数据，转换为低频存储、归档存储或深度归档存储等较冷的存储类型。这样可节省您的存储容量费用，详情请参见 [设置生命周期](https://intl.cloud.tencent.com/document/product/436/14605)。存储类型转换，会产生原存储类型的读请求和目标存储类型的写请求。因此通过生命周期转换存储类型，会产生读写请求费用。关于请求计费说明请参见 [请求费用](https://intl.cloud.tencent.com/document/product/436/40100)。


**注意事项**

- 存储桶中的数据被彻底删除后，将无法恢复，请及时进行数据备份。
- 若存储桶已开启版本控制功能，请暂停版本控制功能后，再执行删除操作。
- 您需要留意费用的结算周期，避免账号产生欠费。若您的计费项均是日结，则清理当天的账单将在您清理后的次日产生。数据彻底清理完成后，系统将不会产生新的费用。详请见 [计费周期](https://intl.cloud.tencent.com/document/product/436/16871)。
- 当您账户余额不足发生欠费（账户余额小于0）时，无论是否处于资源包的有效期，COS 都将在欠费24小时后停止服务。
- 若账号有免费额度，欠费停服后，该资源包将不可使用。
- 若您存储桶中的数据由于违反了相关规定，并且该数据属于二次封禁，则无法删除。如有疑问，请 [联系我们](https://intl.cloud.tencent.com/contact-sales)。 



[](id:guide)

**操作指引**


步骤一：清空存储桶

- 通过 [设置生命周期](https://intl.cloud.tencent.com/document/product/436/14605) 清空存储桶：适用于对象数量大于等于1万个的桶。生命周期策略满足触发条件后，会执行删除任务。任务启动和完成时间，以控制台设置生命周期策略的说明为准。
- 通过控制台 [清空存储桶](https://intl.cloud.tencent.com/document/product/436/30926)：适用于对象数量小于1万个的桶。清空存储桶任务完成后，立即生效。

>? 若您存储桶的数据量较大，在控制台清空存储桶可能会因为网络原因删除较慢或网络断开任务失败，建议您通过设置生命周期清空存储桶。
>

步骤二：删除存储桶

- 通过控制台 [删除存储桶](https://intl.cloud.tencent.com/document/product/436/30361)。
- 通过 [DELETE Bucket](https://intl.cloud.tencent.com/document/product/436/7732) API 删除存储桶。
- 除此之外，您还可以通过 SDK、工具等方式删除存储桶，详情请参见 [删除存储桶](https://intl.cloud.tencent.com/document/product/436/14105)。

步骤三：删除确认

完成步骤一和步骤二后，请您再次登录控制台，确认数据已清理并且桶已删除。存储桶列表为空，则说明您当前账号下无存储桶。

步骤四：费用确认

在您清理存储桶数据后，由于存储容量费用是日结，因此次日账单会体现上一日的存储容量费用。所以请您连续观察清理数据后最近3日的账单，以确保无其他费用产生。

