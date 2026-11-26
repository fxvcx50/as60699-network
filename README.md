# sixtynet as60699 是谁的网络：6 个 /22 网段清单、香港注册主体、零 IPv6 与 RPKI 缺失怎么看？（附官网套餐价格与 abuse 联系方式）

AS60699 的 as-name 是 **SixtyNet**，注册组织为 **CDN1.com Limited**，注册地香港，RIPE 登记，aut-num 创建于 2022 年 6 月 1 日。它名下只有 **6 个 IPv4 前缀，全部是 /22，合计 6,144 个地址**，IPv6 前缀 **0 个**。如果你是拿着日志里的 `111.66.x.x` 或邮件头里的 AS60699 来查底细，上面这几项就是能立刻对上的硬信息。

下面把注册记录、网段归属、路由与健康度、以及官网目前在卖的套餐价格一次列清，最后给出遇到这个 ASN 时该怎么判断。

> **速览**：AS60699 由 SixtyNet 运营，注册主体是香港的 CDN1.com Limited（CR No. 2959031 / BRN 72039483），地址在新蒲岗，abuse 邮箱 `sales@sixtynet.net`。6 个 /22 的 RIPE 描述统一写着“DGOF-BNet Dongguang,Guangdong,China”，但注册地在香港、位置库又测不到任何 IP 落在香港，三套口径互相不重合。RPKI 有效 ROA 为 0/6，没有 IPv6，没有 geofeed。官网 sixtynet.net 在卖 VPS，年付价从 $200 起。
> 👉 [查看 SixtyNet 当前在售套餐与价格](https://sixtynet.net/aff.php?aff=39)

## 注册信息：谁在持有 AS60699

打开 RIPE 的 aut-num 记录，as-name 与 descr 分别写着 SixtyNet 和 SixtyNet LLC，但真正承担法律责任的是 organisation 里的 CDN1.com Limited。

| 项目 | 记录值 |
| --- | --- |
| as-name / descr | SixtyNet / SixtyNet LLC |
| organisation | ORG-CA2355-RIPE |
| org-name | CDN1.com Limited |
| 国家 | HK |
| 注册号 | CR No. 2959031 / BRN 72039483 |
| org-type | OTHER |
| 注册地址 | 210 2/F LAURELS INDUSTRIAL BUILDING 32 TAI YAU STREET SAN PO KONG（香港新蒲岗） |
| abuse 邮箱 | sales@sixtynet.net（abuse-c ACRO59446-RIPE） |
| aut-num 创建 | 2022-06-01T06:21:35Z |
| aut-num 最后修改 | 2025-02-26T08:26:11Z |
| organisation 创建 / 修改 | 2022-05-27T12:48:59Z / 2026-05-13T05:57:30Z |
| status | ASSIGNED |
| mnt-by | RIPE-NCC-END-MNT、MISAKA-MNT、MNT-GFW |

两个细节值得注意。

**abuse 联系人和销售邮箱是同一个地址。** `sales@sixtynet.net` 同时出现在 abuse contact 和 organisation 的 e-mail 字段里。真要投诉滥用，邮件会进销售流程，回复速度和处置流程取决于对方内部怎么分拣，这点心里有数。

**创建日期各家口径略有出入。** aut-num 的 created 字段是 2022-06-01；ip-fd 写 Assigned 2022-05-31、Registered 2022-06-01；TheIpAPI 写 Created 2022-05-29；ipinfo 显示 Allocated 2022-06-01。差几天属于不同数据库对“分配”和“注册”的定义差异，不是记录被改过。另外，部分 WHOIS 页面顶部显示的 `Updated 2026-04-08` 其实是它引用的 as-block（AS60439–AS60807）的时间戳，不是 AS60699 本身的更新时间，别被这个日期误导。

## 网段清单：6 个 /22，6,144 个 IPv4，零 IPv6

| 前缀 | 地址数 | RIPE 描述 |
| --- | --- | --- |
| 111.66.8.0/22 | 1,024 | DGOF-BNet Dongguang,Guangdong,China |
| 111.66.20.0/22 | 1,024 | DGOF-BNet Dongguang,Guangdong,China |
| 111.66.24.0/22 | 1,024 | DGOF-BNet Dongguang,Guangdong,China |
| 111.66.40.0/22 | 1,024 | DGOF-BNet Dongguang,Guangdong,China |
| 111.66.48.0/22 | 1,024 | DGOF-BNet Dongguang,Guangdong,China |
| 111.66.56.0/22 | 1,024 | DGOF-BNet Dongguang,Guangdong,China |
| **合计** | **6,144** | IPv6 前缀：0 个 |

这里有一组必须放在一起看的信息：

- 注册主体在**香港**（RIPE organisation 的 country 字段是 HK，地址在新蒲岗）；
- 六个前缀的描述全部指向**广东东莞**（DGOF-BNet，且该段源自 APNIC 的 portable 分配）；
- ipinfo 的地理位置栏直接写 **“Not active in its registered country”**，即注册在香港，但最近一次测量中没有任何 IP 落在香港。

三条不冲突，它们说的是三件事：谁持有、这段历史描述写的是哪、实际测出来在哪。地理库在前缀没有 geofeed 的情况下只能靠路由和探测反推，SN 注册地与实际部署地分离在托管行业很常见。拿 whois 的国家字段去推断某台机器的延迟或线路，会判断错。

位置稳定性指标可以顺带参考：90 天内保持同一地理归属的比例 100%，一年内 98%，中位迁移间隔 241 天，地理精度到 City。这组数字说明地理库对这个段的标注一直很稳定，但不代表标注就等于机房物理位置。

## 网络健康度：Grade D，50/100

第三方平台 ip-fd.net 给 AS60699 的评分是 **32.7/100，在 123,117 个网络中排第 51,030**。分项里 customer cone 得 0（权重 27%），announced address space 58，peers and providers 23，registry record 70，routing stability 78，RPKI 与 IPv6 两项合计 0（权重 13%）。这个总分被“下游一个网络都没有”和“RPKI/IPv6 双缺”拉得很低。

健康检查 Grade D、50/100，逐项如下：

| 检查项 | 结果 |
| --- | --- |
| 有效 ROA 覆盖 | **0/6**，6 个前缀全部没有 ROA（fail） |
| RPKI invalid 公告 | 无（pass） |
| 是否公告 IPv6 | **不公告**（fail） |
| 上游数量 | BGP 中看到 2 个（pass） |
| abuse 联系可用 | `sales@sixtynet.net` 已公布（pass） |
| 是否发布 geofeed | **无**（fail） |
| 是否公告小于 /24 或 /48 的前缀 | 没有，全部合规（pass） |
| 注册记录维护 | 最后修改 2025-02-26（pass） |

对运维的实际影响：**没有 ROA，也没有 invalid 公告**，意味着目前不会因为 RPKI 校验失败被丢包，但也没有任何加密起源验证保护。如果哪天这段被劫持，靠 RPKI 拦不住，只能靠 IRR 和人工过滤。prefix filter 建议按 IRR 对象走，不要只信 RPKI。

**零 IPv6** 是更硬的短板。六个前缀全是 IPv4，IPv6 NUMs 为 0。你要给这个段做双栈服务、或者在只跑 v6 的环境里访问，这边没有对应资源。

### 上游和对等体的三种说法

同一件事，三个数据库给出三个版本，写清楚比给一个“标准答案”有用：

- ipinfo：**1 个 upstream**（AS136826 PT TITIK TERANG MAKMUR），**2 个 peer**（AS134196 ANYUN INTERNET TECHNOLOGY (HK) CO.,LIMITED、AS136826）；
- ip-fd：BGP 路径里看到 **2 个 upstream**，并记录 **2026-10-19 09:28 UTC，AS136826 的关系由 upstream 变为 peer**；
- ipip 的关联 AS 列表里出现 **AS55933 Cloudie Limited, HK** 与 AS136826。

RIPE 的 aut-num 里还写着路由策略：`from AS57695 accept ANY`、`from AS60068 accept ANY`，`to AS57695 announce AS60699`、`to AS60068 announce AS60699`。也就是说 IRR 里声明的对端是 AS57695 和 AS60068，跟 BGP 实测看到的 AS136826、AS134196 不是同一组。IRR 声明可以滞后于实际配置，这类不一致在中小网络里不算罕见，但你如果要用这段做上游选路或对等互联，必须以自己抓到的 BGP 为准，别照抄 whois。

## 和 Misaka Network 的记录关联

RIPE 记录里能看到几条指向 Misaka Network 的字段：

- `sponsoring-org: ORG-MNI3-RIPE`；
- `mnt-by` 包含 **MISAKA-MNT**（另有 MNT-GFW、RIPE-NCC-END-MNT）；
- `admin-c` 与 `tech-c` 都是 **MNN34-RIPE**，这个 role 名叫 Misaka Network NOC，地址 8 The Green, Suite 6288, Dover, DE 19901, United States，邮箱 `noc@misaka.io`，role 创建于 2017-12-23，最后修改 2018-09-07。

这些只说明注册记录由谁维护、谁做了赞助。资料里没有任何一句写明 SixtyNet 与 Misaka Network 之间存在股权、母公司或品牌归属关系。看到 sponsoring-org 就认定“这是某某旗下”，是把维护关系当成了所有权关系。

## 官网在卖什么：VPS，年付 $200 起

第三方数据库把 AS60699 的 ASN 类型标为 Hosting。官网 sixtynet.net 的产品页叫 VPS Hosting，页面顶部列的产品特性包括 China Unicom Premium AS9929、免费 BGP session、有限 BGP 技术支持、100M 基础带宽、3 倍突发与 95 计费、季付与年付折扣。

当前价格页展示的、能确认套餐名和价格的档位如下（币种 USD，均为年付口径）：

| 套餐 | 核心配置 | 流量 | 年付价格 | 入口 |
| --- | --- | --- | --- | --- |
| Residential-STARTER | 2 核 / 2G RAM / 40G NVMe / 12,500 IOPS / 2G 带宽 / Residential IP | 5TB | 标价 $300，年付 **$260**（省 13%） | [开通 Residential-STARTER](https://sixtynet.net/aff.php?aff=39) |
| LAX-STARTER | 2 核 / 2G RAM / 40G NVMe / 12,500 IOPS / 2G 带宽 / DDOS Protection | 5TB | 标价 $240，年付 **$200**（省 17%） | [开通 LAX-STARTER](https://sixtynet.net/aff.php?aff=39) |
| LAX-MEDIUM | 8 核 / 8G RAM / 160G NVMe / 25,000 IOPS / 10G 带宽 / DDOS Protection | 20TB | 标价 $960，年付 **$800**（省 17%） | [开通 LAX-MEDIUM](https://sixtynet.net/aff.php?aff=39) |
| LAX-LARGE | 8 核 / 16G RAM / 320G NVMe / 25,000 IOPS / 10G 带宽 / DDOS Protection | 40TB | 标价 $1,920，年付 **$1,600**（省 17%） | [开通 LAX-LARGE](https://sixtynet.net/aff.php?aff=39) |

价格页上还能看到若干档位，卡片没标出产品名或没显示价格，包括 Residential 系列的 4 核 4G / 80G / 10TB、8 核 8G / 160G / 20TB、16 核 16G / 320G / 40TB，带 AS9929 中国优化与 Residential IP 的 2 核 2G / 5TB 与 4 核 4G / 10TB，以及一台 4 核 4G、300G + 200G 免费 RAID 10、10TB 流量的存储型配置。这几档的准确名称和报价请以页面当日显示为准，我不在这里替它们编名字。

**买之前必须知道的一条限制**：Residential 系列产品因为 IP 风控原因，**不开放 80 和 443 端口**。想拿住宅 IP 建公开网站，这条路走不通，得看带 DDOS Protection 的 LAX 系列。另外官网对部分住宅产品写明会拒绝所有外部探测与扫描，只允许白名单或端口转发访问。

这正好解释了一个常见疑问：为什么 AS60699 的 6,144 个地址里，最近一次全网扫描中 **0 个 IP 响应 ICMP ping**。产品策略本身就拒探测，扫描测不到回包是预期结果，跟“网络挂了”是两码事。要判断可达性，用具体端口的 TCP 探测比 ping 有用。

👉 [从 SixtyNet 价格页核对最新档位与端口限制](https://sixtynet.net/aff.php?aff=39)

## 关于 CDN1 这个名字的一点补充

AS60699 的注册组织名是 CDN1.com Limited。第三方测评曾对 CDN1 这个品牌提出过信任层面的质疑，包括其 CDN 业务使用开源 GoEdge 架构、官网 SSL 证书过期未续、以及与某些恶意脚本基础设施在迁移时间上的重合。那篇测评里写的 CDN1 的 ASN 是 **AS154206**，跟本篇的 AS60699 不是同一个 ASN，IP 段也不在同一批。

我把这段放进来，是因为你查 AS60699 时早晚会看到 CDN1 这个名字，提前知道它背后有争议报道，比事后自己撞上要好。这些指控来自第三方博客，没有经过独立证实，也不构成对 AS60699 这段网络的定性。

## FAQ

**AS60699 到底归谁？**
RIPE 记录上 as-name 是 SixtyNet，descr 是 SixtyNet LLC，承担责任的 organisation 是 CDN1.com Limited，注册地香港，注册号 CR No. 2959031 / BRN 72039483。

**为什么 IP 归属地一会儿香港、一会儿东莞、一会儿洛杉矶？**
三个来源说三件事：注册地在香港（RIPE），六个前缀的 RIPE 描述写东莞，官网在卖的主力产品标着 LAX（洛杉矶）与 AS9929 中国优化线路。加上这个段没有发布 geofeed，地理库只能猜。

**有 IPv6 吗？**
没有。IPv6 前缀 0 个，IPv6 地址数 0。

**被 111.66.x.x 扫了或者收到这个段的滥发邮件，找谁？**
`sales@sixtynet.net`，这是 RIPE 记录里公布的 abuse 联系地址（abuse-c ACRO59446-RIPE）。注意它同时也是销售邮箱，邮件标题写清是 abuse 报告，附上时间戳、源 IP、目标端口和日志片段，处理会快一些。

**0 个 IP 响应 ping，是不是这段已经废弃了？**
不是。官网明确写了部分产品拒绝所有外部探测与扫描，只对白名单或端口转发开放。ping 不通不能推出网络不可用，要验证就用业务端口做 TCP 连接测试。

## 该不该继续往下查，看你的场景

把这篇文章的信息压成几条判断规则：

- **只是想知道日志里的 IP 是谁**：AS60699 = SixtyNet，注册主体 CDN1.com Limited（香港），6 个 /22 共 6,144 个 IPv4，无 IPv6。到此够了。
- **要做滥用投诉**：发 `sales@sixtynet.net`，附完整日志。别指望它自动分流到专门的 abuse 团队。
- **要把它加进上游或做对等**：先自己抓 BGP。IRR 里声明的 AS57695 / AS60068 和实测的 AS136826 / AS134196 对不上，WHOIS 的路由策略不能直接当配置依据。
- **要做 RPKI 严格校验**：这段 6 个前缀全部没有 ROA，你没有可依赖的起源验证，只能靠 IRR 过滤。
- **要买机器**：住宅 IP 系列不开放 80/443，建站选 LAX 系列；只需最小配置就从 LAX-STARTER 的 $200 年付起步，8 核 8G 以上的需求才轮到 LAX-MEDIUM 及以上。下单前在结账页确认当时的支付方式和计费周期，价格页展示的是年付口径。

👉 [前往 SixtyNet 查看当前套餐与年付价格](https://sixtynet.net/aff.php?aff=39)
