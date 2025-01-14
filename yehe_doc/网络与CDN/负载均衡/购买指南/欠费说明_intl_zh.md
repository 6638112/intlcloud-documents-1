## 按量计费
>?
>- 按量计费资源不再使用时**请及时删除** ，以免继续扣费。
>- 您的实际资源消耗可能不断变化，因此余额预警可能存在一定的误差。

![](https://staticintl.cloudcachetci.com/yehe/backend-news/6GWe135_PRELIM__%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1_%E4%BA%A7%E5%93%81%E7%9B%AE%E5%BD%95_%E4%B8%AD%E8%AF%91%E8%8B%B1_EN-US.png)

### 余额预警
系统每天会根据您名下按量付费资源在过去24小时的消费情况以及账户余额情况，预估余额可支撑的时间。若可支撑时间小于5天，系统将会向您推送余额预警消息。预警消息将通过已设置的开启方式（例如邮件、短信、站内信等），通知到腾讯云账户的创建者及已订阅消息的协作者。

### 欠费预警
按量计费资源每个整点进行结算。在您的账户被扣为负值时（上图中点1），预警消息将通过已设置的开启方式（例如邮件、短信、站内信等），通知到腾讯云账户的创建者及已订阅消息的协作者。

### 欠费处理
- 从您的账户余额被扣为负值时刻起，按量计费负载均衡在24小时内可继续使用且继续扣费，24小时后（上图中点2）负载均衡将进入隔离状态，实例被隔离后将作停服处理（服务不可用，仅保留配置数据）且停止扣费，续费后恢复服务。
- 若停服后，账户隔离超过7天系统将释放负载均衡实例，实例释放后，相关配置等数据将被永久删除，不可恢复。

>!负载均衡不会主动解除与 CVM 的绑定关系，当**云服务器**进入隔离状态（按量计费云服务器欠费两小时以上）时，也**不会解除**与 CLB 的绑定关系。
>

