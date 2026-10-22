# 发布指南 —— 把账本模板发到 GitHub 和 TradingView

> 这份指南是写给发布者本人（Kok）的操作清单：每一步一句话，照着点就行。
> **所有涉及账号的点击都必须你本人在自己的账号上完成**，助手只能把文件和文案备好。
> 你的 GitHub 账号是 **xzhangdada-beep**；注意：`jarvis-quant` 是另一个项目的仓库，
> 这次要**新建一个仓库**，不要把账本文件传进 jarvis-quant 里。

---

## 一、GitHub 发布（约 5 分钟）

1. 打开 github.com 并登录你的账号（xzhangdada-beep）。
2. 点页面右上角的「+」号，选择「New repository」。
3. 仓库名填 `ord-ledger`，下面选 **Public**（公开，任何人可见可下载）。
4. 点最下面的「Create repository」，仓库就建好了。
5. 在新仓库页面点「uploading an existing file」这行小字链接。
6. 把发布包的 5 个文件拖进上传框（清单见文末），等它们都传完。
7. 在页面下方的「Commit changes」区域，标题就写一句：`ORD 账本模板 v1.0 首发`，点绿色按钮确认。
8. 回到仓库主页，点右侧 About 旁的齿轮图标，把仓库描述填上这句：
`给任何 Pine 指标加一本可导出、可逐笔对账的账（CFG/ORD/HOL）· Drop-in auditable per-trade ledger for Pine Script indicators`
9. 完成 —— 把仓库链接记下来，TV 发布时要用（见第二节第 6 步）。

**上传文件清单（5 个，都在发布包里）：**

- `ord_ledger_template.pine`（模板本体 + 演示宿主）
- `INTEGRATION_GUIDE.md`（接入指南）
- `README.md`（说明与格式规范）
- `LICENSE`（MIT 许可）
- `PUBLISH_GUIDE.md`（就是本文件，方便以后照着更新版本；可传可不传）

> `RELEASE_CHECKLIST.md` 是内部核对件，**不用上传**。

---

## 二、TradingView 发布（免费开源公开脚本）

1. 打开 TradingView 图表，点开下方的「Pine 编辑器」，新建一个空白脚本。
2. 把 `ord_ledger_template.pine` 的全文粘贴进去（它自带 EMA 交叉演示宿主，是一个完整可运行的指标）。
3. 先点「添加到图表」看一眼：右上角出现状态小表、图上有 Buy/Sell 标签，就是工作正常。
4. 点编辑器右上角的「发布脚本」，在发布窗口里选 **开源 / Open-source**（源代码公开、免费、所有人可用）——
不要选 invite-only（那是收费脚本的路，规则完全不同，这次不走）。
5. 标题和描述用第三节的现成草稿，整段粘贴，不要自己加词（尤其不要加任何收益类形容词，原因见第四节）。
6. 描述草稿最后一行有个 GitHub 链接占位，发布前把第一节建好的仓库地址粘进去替换掉。
7. 点发布，审核通过后脚本就出现在你的 TV 主页和公共脚本库里。
8. 把发布后的 TV 脚本链接记下来 —— 和 GitHub 链接互相回填（见第五节）。

---

## 三、TradingView 标题与描述草稿（直接粘贴）

**标题：**

```
ORD Ledger Template — Auditable Per-Trade Log for Any Pine Indicator
```

**描述：**

```
ORD Ledger Template (with EMA-cross demo host)
给任何 Pine 指标加一本可导出、可逐笔对账的账。

This is a drop-in ledger block for indicator() scripts. It records every
simulated trade as a CSV row in the Pine Logs:
- a CFG header line that self-certifies the script's parameters and timeframe,
- one ORD row per closed trade (entry/exit time and price, exit reason,
gross/net R after fees, net U, bars held),
- a HOL snapshot row for the position still open at the data end.

Why: TradingView gives strategy() scripts a built-in trade list, but
indicator() scripts get nothing — no ledger, no trade list, no reconciliation.
With this ledger, every trade your indicator makes on the chart can be
exported and checked line-by-line against an external backtest engine.
No trade exists unless it is in the ledger.

How to use: copy the template block from the GitHub repo into your own
indicator, then call three functions at your signal/entry/exit events:
f_ord_signal(), f_ord_open(), f_ord_close(). The EMA crossover in this
script is only a demo host — delete it and keep the ledger block.

Scope: this template only does accounting and export. It makes no
performance claims, and the host indicator's signals and logic remain
entirely its author's. Default fee 0.05%/side; the R distance is defined
by the host at entry (see the repo docs for the format spec).

Format spec & integration guide (GitHub):
License: MIT (ledger template).
```

---

## 四、合规要点（花一分钟看完，能省很多麻烦）

- **描述里绝不能出现收益承诺类字样**：不写胜率、不写收益率、不写「 profitable / make money /
稳定盈利 / 月入多少」这类词。咱们这个脚本是**记账工具**，文案只讲「记什么账、格式是什么」，
一个字的交易效果都不提 —— 这既是 TV 社区规则的要求，也是这套账本的本分：
它证明的是数字对得上，不是能赚钱。
- 同理，不要在描述里贴回测收益截图或净值曲线图；发布时附的图表截图就是演示图本身即可。
- 选「开源」发布后，源码所有人可见、可抄 —— 这正是「造福大家」的目的，模板本身是 MIT，
别人用它不需要再问你。但注意：这条只适用于账本模板，**你自己的其他指标不要顺手一起公开**。
- 发布后如果有人留言问「能不能赚钱」，标准答复就是描述里那句：这是记账工具，不做收益承诺。

---

## 五、发布后回填链接（两个平台互相指路）

1. GitHub 仓库建好后，先把仓库链接填进 TV 描述草稿的最后一行占位处（第二节第 6 步），再发 TV。
2. TV 发布成功后，把 TV 脚本链接填回 GitHub 的 `README.md`：
打开仓库里的 `README.md` → 点右上角铅笔图标（Edit）→ 在「已落地实例」表格里
新增一行：`ORD 账本模板 · TV 演示版 | 本仓库模板的 TradingView 公开演示 | ` → 点 Commit。
（嫌麻烦的话，把两个链接发回给助手，由助手把改好的 README 递给你，你只需上传覆盖这一个文件。）
3. 两个链接都回填完，这次发布才算闭环。
