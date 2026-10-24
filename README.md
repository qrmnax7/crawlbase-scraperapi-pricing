# crawlbase api：定价、credit 成本拆解，以及一个值得对比的 ScraperAPI 替代方案

搜 "crawlbase api" 的大多是同一类人：手里有个抓取任务，想知道这个 API 到底怎么计费、一个 credit 能换多少页面、以及有没有更便宜的选择。先把答案放在最前面：Crawlbase 的 Crawling API 按“成功请求”计费，标准请求 1 credit，订阅从 $99/月起，也支持 $0 月费的按量付费；但如果你的目标站带 JS 渲染或高强度反爬，实际单价会被倍率放大很多。这时候值得把 ScraperAPI 这类同类抓取 API 拉进来比一比——它的免费试用给得更直接，官网甚至内置了一个工具帮你算真实单页成本。

> **选购速览**：多数中小型抓取项目（月量 2 万–20 万页、目标以普通电商和搜索页为主）选 ScraperAPI 的 Hobby（$49/月，100,000 credits）就够用；注册有 7 天 5,000 credits 试用，7 天内不满意可直接退款。👉 [查看 ScraperAPI 全部套餐与当前价格](https://www.scraperapi.com/pricing/?fp_ref=coupons)

## Crawlbase API 是什么，能做什么

Crawlbase 的核心产品是 Crawling API：你发送目标 URL，它通过代理池抓取页面，返回 HTML 或解析后的 JSON，内置 CAPTCHA 和反爬处理，另支持全页截图。同一套 credits 余额覆盖四条产品线——Crawling API（含截图）、Crawler、Smart AI Proxy 和 Cloud Storage，共用一张费率卡。

认证用双 token 模型：Normal Token 处理静态 HTML 和 JSON 端点，速度快、成本低；JavaScript Token 处理 SPA 和懒加载页面，走真实浏览器渲染。官方还提供 PHP、Node.js、Go 等 SDK，并支持把全部工具接入 Claude、Cursor 等 MCP 兼容客户端。

一个对预算友好的细节：Crawlbase 官方明确“只对成功请求计费”，被封锁或失败的请求不计入账单，无论目标站或渲染模式如何。这一点在同类产品里并不多见。

## Crawlbase API 怎么收费：按量 + 订阅两套体系

Crawlbase 所有账户默认按量付费：$0 月费、无需信用卡，按月后付（billed in arrears），可设硬性消费上限。标准请求的阶梯费率从每 1,000 次 $3.00 一路降到 $0.02。

官方给出的标准请求算例：

| 月成功请求量 | 按量总成本 | 折合每千次 |
| --- | --- | --- |
| 100K | $76.40 | ≈ $0.76 |
| 1M | $527.50 | ≈ $0.53 |
| 10M | $1,471.90 | ≈ $0.15 |

如果量级稳定，订阅制更划算。四档订阅如下（超出额度后按你已达到的阶梯继续按量计费）：

| 套餐 | 月 credits | 月付 | 年付（享 1 个月免费，约 8% 折扣） | 折合每千 credits |
| --- | --- | --- | --- | --- |
| Starter | 200,000 | $99 | $1,089/年 | ≈ $0.50 |
| Scale 500K | 500,000 | $199 | $2,189/年 | ≈ $0.40 |
| Scale 1M（Most popular） | 1,000,000 | $349 | $3,839/年 | ≈ $0.35 |
| Growth | 2,000,000 | $599 | $6,589/年 | ≈ $0.30 |

超过 2M credits/月需要走企业定制（含 SLA 和发票结算）。所有档位（含按量付费）都包含住宅代理轮换和 CAPTCHA 处理，不额外收费，还有 100+ 内置爬虫（结构化 JSON 与原始 HTML 同价）。

新账户自带 1,000 免费 credits，无需绑卡；完成账户设置步骤后可以涨到最多 5,000。

## 真实成本陷阱：站点难度倍率和 JS 渲染

Crawlbase 的标价只是起点。两个系数会放大实际账单：

1. **JS 渲染 ×2**：真实浏览器渲染让任何请求的 credits 翻倍，没有单独的浏览器档位。
2. **站点难度倍率**：官方把站点分成八档，从 Standard ×1 到 Extreme II ×20，重度防护站点自动套用更高档位，倍率作用于该组阶梯总额。两者叠加时，一个 Extreme 档 + JS 渲染的请求消耗的 credits 是标准请求的 18 倍。

这意味着 Starter 的 200,000 credits 在简单站点上能跑 20 万个页面，换成强防护站点的渲染请求，可能只够几万个。订阅页面上“每千 credits 单价”是理想情况下的数字，估算预算时要把你自己目标站的档位算进去。

## 对比 ScraperAPI：定价逻辑不同，免费试用更直接

ScraperAPI 是同一赛道的产品：单个 HTTP 端点，附带 API key 和目标 URL，代理轮换、重试、验证码和 JS 渲染由服务端处理。官方宣称代理池超过 4,000 万 IP，覆盖住宅、数据中心、移动三类网络、50+ 国家。

它和 Crawlbase 的关键区别在计费模型：ScraperAPI 按订阅套餐卖固定 credits 包，不按量后付，也不按阶梯降价。全套餐如下（年付 9 折）：

| 套餐 | 月付 | 年付折后月价 | Credits/月 | 并发线程 | 地理定位 | 购买 |
| --- | --- | --- | --- | --- | --- | --- |
| Hobby | $49 | $44.10 | 100,000 | 20 | 仅 US & EU | [ 开通 Hobby 套餐](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| Startup | $149 | $134.10 | 1,000,000 | 50 | 仅 US & EU | [ 开通 Startup 套餐](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| Business | $299 | $269.10 | 3,000,000 | 100 | 国家级 | [ 开通 Business 套餐](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| Scaling（Most popular） | $475 | $427.50 | 5,000,000 | 200 | 国家级 | [ 开通 Scaling 套餐](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| Professional | $975 | $877.50 | 10,500,000 | 300 | 国家级 | [ 开通 Professional 套餐](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| Advanced | $1,975 | $1,777.50 | 21,500,000 | 500 | 国家级 | [ 开通 Advanced 套餐](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| Enterprise | 定制 | 定制 | 22,000,000+ | 500+ | 国家级 | [ 联系销售定制方案](https://www.scraperapi.com/pricing/?fp_ref=coupons) |

所有套餐（含免费层）都带 JS Rendering、Premium Proxies、JSON Auto Parsing、CAPTCHA 与反爬处理、无限带宽和 99.9% 正常运行时间保证；付费套餐另含结构化数据 API（Amazon、Google、Walmart 等直接返回解析 JSON）、DataPipeline 定时任务、完整 Crawler 访问和按量付费选项。

免费层比 Crawlbase 更“可测”：注册即得每月 1,000 免费 credits（5 个并发），**注册后前 7 天另有 5,000 免费请求**用于更大规模测试，无需信用卡。加上官方的 7 天无条件退款政策（"no questions asked"，联系支持即可办理）和随时免费取消订阅，试用成本几乎为零。👉 [用 7 天免费试用跑一遍你的目标站](https://www.scraperapi.com/pricing/?fp_ref=coupons)

## Credit 消耗规则：ScraperAPI 把账算在了明面上

这是本文最值得记住的一节，也是多数对比文章没讲透的地方。

ScraperAPI 的 credit 倍率是公开且具体的：标准页面 1 credit，**Amazon 5 credits，Google 和 Bing（含子域名）25 credits，LinkedIn 30 credits**；Cloudflare、Datadome、PerimeterX 这类防护站点每次绕过加收 10 credits。JS 渲染（`render=true`）按第三方实测口径约 10 credits。

听起来吓人，但官方给了两个自救工具：

- **Domain Cost Estimator**：dashboard 里可以对任意 URL 查询精确 credit 成本，下单前先算账。
- **`max_cost` 参数**：给单次抓取设成本上限，防止一个失控的请求烧掉一大块额度。

实际影响可以这样理解：在 Startup 的 100 万 credits 里，抓普通 HTML 页面就是 100 万页；如果任务是“Amazon 搜索结果页 + JS 渲染”，第三方评测估算同样的 credits 只能覆盖约 4 万–10 万个真实页面。结论和 Crawlbase 那边一样——**按真实单页成本做预算，别按套餐标题上的 credit 数**。

两家在这点上其实殊途同归：Crawlbase 用站点难度倍率（最高 ×20），ScraperAPI 用按域名定价（Google 25、LinkedIn 30），复杂目标的溢价都是真实存在的。区别是 ScraperAPI 把常见域名的具体倍率直接写进了定价页，你不用猜。

## 几个只写在文档里的限制，买之前先知道

这部分信息对决策影响不小，但在多数营销页面上找不到。

**ScraperAPI 侧：**

- Credits 按月过期，不结转。季度性大批量抓取（比如每季度跑一次大爬取）会为闲置月份付费。
- 超额处理分档：Hobby 到 Professional 可以开启 opt-in 的 Auto-Upgrade，credits 用尽自动升到下一档（单 credit 价格通常更优）；Scaling 及以上支持 Pay-As-You-Go 按固定单价续用，可设月度消费上限——注意这个上限是限额，不会预先扣款。
- 低于 Scaling 的套餐没有按量续费选项。用量贴近 Startup 上限时要么升到 Business（$299），要么靠 `max_cost` 和精简渲染把消耗压回去——这是套餐阶梯里最陡的一步（$149 → $299）。
- 超出并发线程上限返回 429，请求直接拒绝而非排队，不加收费用。
- Hobby 和 Startup 的地理定位仅限美国和欧盟；美国、欧盟以外的国家级定位需要 Business（$299）起。
- `session_number` 粘性会话大约维持 1 小时，做跨天保持身份的场景（账号抓取、广告验证）不合适。
- 无法指定具体 IP、ASN 或城市，只能选国家、会话和 IP 档位——需要这种粒度的话，裸代理更合适。
- 不按带宽计费，只按请求数计费；也不能单独购买代理 IP。

**Crawlbase 侧**对应的优势和限制：成功才计费（失败请求不扣 credits）对不稳定目标更宽容；订阅超出额度后按已达阶梯继续按量，不用换套餐；按量付费模式自带硬性消费上限。但它的 JS 渲染固定 ×2、难度倍率自动套用，强防护站点的账单弹性同样很大。

## ScraperAPI vs Crawlbase：一张表看核心差异

| 维度 | ScraperAPI | Crawlbase |
| --- | --- | --- |
| 最低付费门槛 | $49/月（Hobby） | $0（按量付费默认开启） |
| 付费起点订阅 | $49/月，10 万 credits | $99/月，20 万 credits |
| 100 万标准请求成本 | $149（Startup 套餐内） | ≈ $527.50（按量）或 $349（Scale 1M 订阅） |
| 失败请求 | 文档未说明计费豁免 | 明确不计费 |
| 免费额度 | 每月 1,000 + 7 天 5,000 试用 | 1,000 起，完成设置可到 5,000 |
| 退款 | 7 天无条件退款 | 资料未载明 |
| 反爬站点成本 | 按域名定价（Google 25、LinkedIn 30、防护绕过 +10） | 难度倍率 ×1 至 ×20 |
| 地理定位 | Business 起支持美国/欧盟以外国家级 | 资料未载明分层限制 |

要提醒一句：两家的 "credit" 定义并不完全等价，上面的对比是按各自官方口径并列呈现，不能直接换算成“谁便宜 3.5 倍”。ScraperAPI 的套餐价对应的是 credit 包上限，Crawlbase 按量价对应的是实际成功请求数。

## 怎么选：按你的目标站类型定

判断标准只有一个：你的目标站长什么样、量有多大。

- **普通电商页、SERP、公开数据站，月量 2 万–20 万页**：ScraperAPI 的 Hobby 或 Startup 足够，默认代理池就能过大多数请求，用不上昂贵的 premium 档。👉 [用免费试用先验证你的目标站能不能抓](https://www.scraperapi.com/pricing/?fp_ref=coupons)
- **需要解析后的结构化 JSON（Amazon、Google、Walmart）**：ScraperAPI 的结构化端点省掉自维护解析器的时间；Crawlbase 也有 100+ 内置爬虫，两者能力相近，看哪家覆盖你的目标站更全。
- **目标重度反爬（强防护站点 + 渲染）且量很大**：两家都会贵，Crawlbase 的按量模式让低频试探几乎零成本，ScraperAPI 的 7 天退款窗口更适合先跑真实任务再决定。
- **需要美国/欧盟以外精确到国家的定位**：ScraperAPI 要上到 Business（$299）；如果预算卡在 $150 以内，这个限制会直接决定选择。
- **完全不想付月费、用量极不规律**：Crawlbase 的 $0 按量付费是它的独有优势，ScraperAPI 没有对应模式。

下单前最后确认两件事：一是用各自官方的成本估算工具（ScraperAPI 的 Domain Cost Estimator 或 Crawlbase 的费率计算器）跑一遍你真实的目标 URL，拿到单页 credit 数再乘以月量；二是记好 ScraperAPI 的 7 天退款期限——试用期内跑真实任务，不满意直接找支持退款，这是同类产品里最干脆的退出机制。👉 [查看 ScraperAPI 定价并开始 7 天试用](https://www.scraperapi.com/pricing/?fp_ref=coupons)

## FAQ

**Crawlbase API 的 JS 渲染额外收多少？**
真实浏览器渲染让任何请求的 credits 翻倍（×2），没有单独的浏览器套餐档位，且与站点难度倍率叠加。

**ScraperAPI 有免费试用吗？**
有。注册后 7 天内可用 5,000 免费请求，无需信用卡；之后还有每月 1,000 免费 credits 的免费计划（5 个并发）。7 天内购买后不满意可申请无条件退款。

**Crawlbase 按量付费需要预充值吗？**
不需要。$0 月费、无信用卡，按月后付，只为成功请求付费，可设硬性消费上限。

**两家哪家的免费 credits 更多？**
名义数字接近（ScraperAPI 试用 5,000、Crawlbase 完成设置后最高 5,000），但结构不同：ScraperAPI 的 5,000 集中在 7 天内用完，适合短时间高强度验证；Crawlbase 的额度随设置步骤逐步解锁，更像长期免费层。
