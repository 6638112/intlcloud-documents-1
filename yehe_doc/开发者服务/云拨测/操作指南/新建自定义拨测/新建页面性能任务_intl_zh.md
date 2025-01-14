该任务用于 Web 页面性能体验场景，可以获取用户在不同的运营商、城市地域、浏览器版本、操作系统、设备等环境下，访问 Web 页面的体验数据，全面了解页面的性能。本文将为您介绍如何新建页面性能任务。

## 操作步骤

1. 登录 [云拨测控制台](https://console.cloud.tencent.com/cat/probe/tasklist)。
2. 在左侧菜单栏中单击**任务列表**。
3. 单击任务列表页面上方的**新建任务**。
4. 根据下列说明配置基本信息。
<table>
<tr>
<th> 配置项</th>
<th> 说明</th>
</tr>
<tr>
<td> 拨测类型</td>
<td> 选择“自定义拨测”</td>
</tr>
<tr>
<td> 任务类型</td>
<td> 选择 PC 端或移动端“页面性能”任务类型</td>
</tr>
<tr>
<td> 拨测地址</td>
<td> 请填写需要拨测的 Web 应用地址（以 <code>http://</code> 或 <code>https://</code> 开头）<br>例如：<br/>1. 域名:http://www.tencent.com<br/>2.
域名端口：http://www.tencent.com:80<br/><b>说明：</b>Ping监测下使用TCP或UDP协议时，需要填写端口。
</td>
</tr>
<tr>
<td> 拨测任务名称</td>
<td> 自定义拨测任务名称</td>
</tr>
<tr>
<td> 拨测频率</td>
<td> 支持1分钟、5分钟、10分钟、15分钟、30分钟、60分钟、120分钟的拨测频率。例如选择5分钟频率，表示每个拨测点每5分钟拨测一次</td>
</tr>
<tr>
<td> 执行时间</td>
<td> 默认每日按频率执行，您也可根据需求自定义执行计划。例如您可以设置每周上午8点-9点执行拨测任务</td>
</tr>
<tr>
<td> 任务标签</td>
<td>云拨测结合腾讯云资源标签功能，为您提供按标签授予子账号权限和按标签分账功能。详情可参见 <a href="https://www.tencentcloud.com/document/product/1169/52017">资源标签</a> 进行配置 </td>
</tr>
</table>
5. 根据下列说明配置拨测点。
    i.选择方式：选择推荐拨测点组或自定义拨测点组（推荐的拨测节点为常用的节点）。
    ii.选择拨测点：
	- 可用性拨测点组：仅支持网络质量、端口性能任务类型，适用于网络质量监控、接口可用性监控、劫持和封堵检测。
	- 高级场景拨测点组：页面用户体验监控、直播卡顿监控、弱网环境可用性探测、CDN 选型与路径优化。覆盖境内外的 IDC、PC 终端、移动端探测点。
     - 推荐拨测点组：为您推荐常用拨测点组。
     - 自定义拨测点组：**选择拨测点地域** > **选择拨测点类型** > 在右侧框中勾选拨测点。拨测点类型说明如下：
<table>
<tr>
<th> 拨测点类型</th>
<th> 说明</th>
</tr>
<tr>
<td> 机房（IDC）</td>
<td> 部署在 PC 电脑上的拨测点，代表 PC 用户体验。</td>
</tr>
<tr>
<td> 网民（LastMile）</td>
<td> 部署在终端用户 PC 电脑上的拨测点，代表终端 PC 用户体验。</td>
</tr>
</table>
 - 我的拨测点组：您可以在“高级场景拨测点”中选择常用的拨测点组，并单击右下角的**新建拨测点组**即可。下次创建任务时，直接选择我的拨测点组，即可快速选择您创建的常用拨测点。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/syUR261_28intl_%E5%A5%BD%E5%8E%8B%E7%9C%8B%E5%9B%BE.png)
<dx-alert infotype="explain" title="选择建议">
由于机房（IDC）和网民（LastMile）网络环境不同，机房（IDC）比网民（LastMile）更稳定。

- 若是要监测业务的可用性，可以选择比较稳定的机房 IDC。
- 若要看终端用户的访问体验、网络情况等建议多选网民 LastMile 或移动端，可以模拟终端用户访问应用的体验。
</dx-alert>
6. 配置拨测参数（可选），系统默认为您配置常用的拨测参数，您也可以自定义拨测规则。配置说明如下：
<table>
<tr>
<th> 配置项</th>
<th> 说明</th>
<th> 默认取值</th>
</tr>
<tr>
<td> IP 类型</td>
<td> 支持自动、IPV4、IPV6 三种 IP 协议类型</td>
<td> 自动</td>
</tr>
<tr>
<td> 自定义 Host</td>
<td> 支持按 IP 地址轮询或随机监测，多个 IP 请用半角逗号分隔符，<br>例如：<ul style = "margin-bottom: 0px;">
<li>IPv4：<code>192.168.2.1,192.168.2.5:img.a.com&#124;192.168.2.1?]:img.a.com&#124;</code></li><li>IPv6：<code>[0:0:0:0:0:0:0:1][8080],[0:0:0:0:0:0:0:2][8081]:www.a.com|]</code></li></ul></td>
<td> -</td>
</tr>
<tr>
<td>流量劫持（识别元素）</td>
<td>当页面发生 302 重定向时，若重定向页面元素超过该设定值，则认为页面被劫持。劫持详情可在 <a href="https://console.intl.cloud.tencent.com/cat/analyze">多维分析页面</a>勾选查看。
<td> -</td>
</tr>
<tr>
<td>流量劫持（劫持标识）</td>
<td>设置匹配的关键信息。流量劫持功能，针对浏览页面时302跳转情况进行分类统计。（监测前提是页面中有302的元素，一般监测基础文档发生302后的情况）  </td>
<td> -</td>
</tr>
<tr>
<td>页面篡改</td>
<td>代表出现了域名设置之外的元素都属于页面被篡改。常见的表现形式为弹出广告、浮动广告、跳转等行为。  </td>
<td> -</td>
</tr>
<tr>
<td>DNS 劫持白名单</td>
<td> 当任务的目标 IP 在 DNS 白名单内，则认定为没有发生了 DNS 劫持，详情请参见 <a href="https://www.tencentcloud.com/document/product/1169/52000">劫持监测参数说明</a>。 </td>
<td> -</td>
</tr>
<tr>
<td>DNS 劫持黑名单</td>
<td>  当任务的目标 IP 在 DNS 黑名单内，则认定为发生了 DNS 劫持，详情请参见 <a href="https://www.tencentcloud.com/document/product/1169/52000">劫持监测参数说明</a>。</td>
<td> -</td>
</tr>
</table>

