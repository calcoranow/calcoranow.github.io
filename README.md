# Calcora

**在线地址：[https://calcoranow.com](https://calcoranow.com)**

Calcora 是一个纯浏览器端运行的在线计算器集合，覆盖数学、金融、健康、单位换算、时间、编程、电学、物理、天文等 17 个分类，共 **380+ 个工具**。所有计算都在你的设备上完成——输入不会被上传，没有账号，没有服务端参与运算。

> 本仓库（`calcoranow.github.io`）是 Calcora 的项目主页仓库；应用源码位于 [`calcnate/calculators`](https://github.com/calcnate/calculators)。

---

## 目录

- [它解决什么问题](#它解决什么问题)
- [核心特性](#核心特性)
- [工具分类](#工具分类)
- [技术栈](#技术栈)
- [本地运行](#本地运行)
- [构建与部署](#构建与部署)
- [项目结构](#项目结构)
- [新增一个计算器](#新增一个计算器)
- [产品边界](#产品边界)
- [License](#license)

---

## 它解决什么问题

网上的计算器大多被广告、弹窗、注册墙和"下载 App"打断，而且很多把简单公式包装成需要联网的接口。Calcora 的做法相反：

- **一个公式一个页面**，打开就能算，默认值已经填好，首屏就有结果；
- **输入即状态**，参数同步到 URL hash，把链接发给别人，对方看到的是同一组数字和同一个结果；
- **能力诚实**：只做有确定公式的计算，不做"实时汇率""按年更新的税率表"这类会过期的假数据。

## 核心特性

| 特性 | 说明 |
| --- | --- |
| 纯前端计算 | 静态导出（`output: "export"`），无服务端、无 API 调用，计算不离开浏览器 |
| 隐私优先 | 无账号、无 Cookie、无统计脚本、无指纹采集 |
| 可分享的结果 | `useHashState` 把数值/枚举输入写入 URL hash，刷新和转发都不丢状态 |
| 全站搜索 | 首页与 `/all` 共用一个可搜索目录，支持别名（`aliases`）命中，例如搜 "hcf" 也能找到 GCD/LCM |
| 分类导航 | 17 个顶层分类，每个分类有独立索引页与网格视图 |
| SEO 就绪 | 每个工具由脚本生成独立 `layout.tsx`（title / description / canonical / OG / JSON-LD），并自动生成 `sitemap.xml` 与 `robots.txt` |

## 工具分类

| 分类 | 直达 | 工具数 | 代表工具 |
| --- | --- | ---: | --- |
| Finance 金融 | [/finance](https://calcoranow.com/finance) | 79 | 房贷、车贷、贷款、复利、APR/APY、CD、401k、VAT、小费 |
| Math 数学 | [/math](https://calcoranow.com/math) | 50 | 通用/科学计算器、百分比、分数、指数对数、质数、方程 |
| Everyday 日常 | [/everyday](https://calcoranow.com/everyday) | 47 | 平方英尺、混凝土、工时表、油耗、屋顶坡度 |
| Health 健康 | [/health](https://calcoranow.com/health) | 30 | BMI、TDEE、BMR、宏量营养素、体脂、孕期 |
| Computer 编程 | [/computer](https://calcoranow.com/computer) | 24 | JSON、哈希、Cron、颜色、宽高比、IBAN 校验 |
| Conversions 换算 | [/conversions](https://calcoranow.com/conversions) | 23 | 长度/重量/温度/体积/面积/速度/时间，含统一换算器 |
| Physics 物理 | [/physics](https://calcoranow.com/physics) | 22 | 密度、速度、能量、功率、压强 |
| Electricity 电学 | [/electricity](https://calcoranow.com/electricity) | 19 | 欧姆定律、压降、kVA↔A、线径、电费 |
| Space 天文 | [/space](https://calcoranow.com/space) | 16 | 轨道、相对论、天文单位与观测 |
| AI | [/ai](https://calcoranow.com/ai) | 12 | 模型显存/吞吐估算、Token 与上下文成本 |
| Geometry 几何 | [/geometry](https://calcoranow.com/geometry) | 11 | 平面图形面积、周长、体积 |
| Timers 时间 | [/timers](https://calcoranow.com/timers) | 10 | 日期差、年龄、时长、时区 |
| Statistics 统计 | [/statistics](https://calcoranow.com/statistics) | 10 | 分布、置信区间、z/t 检验、概率 |
| RF & Antenna 射频 | [/rf](https://calcoranow.com/rf) | 10 | 天线长度、链路预算、驻波比 |
| Network 网络 | [/network](https://calcoranow.com/network) | 9 | 子网划分、带宽、Wi-Fi 信道、端口 |
| Security 安全 | [/security](https://calcoranow.com/security) | 7 | 密码强度、JWT、哈希、WebAuthn |
| Education 教育 | [/education](https://calcoranow.com/education) | 7 | GPA、成绩与学习规划 |

完整清单见 [/all](https://calcoranow.com/all)。

## 技术栈

- **框架**：Next.js 16（App Router）+ React 19，启用 React Compiler
- **语言**：TypeScript
- **样式**：Tailwind CSS 4
- **图标与图表**：lucide-react、Recharts（仅部分金融页面）
- **渲染模式**：`output: "export"` 全静态导出到 `out/`
- **托管**：Cloudflare Workers 静态资源（`wrangler.toml` 的 `[assets]` 指向 `./out`），历史方案 AWS CDK 仍保留在 `infra/`

## 本地运行

```bash
npm install
npm run dev
```

打开 [http://localhost:3000](http://localhost:3000)。

其他常用命令：

```bash
npm run lint          # ESLint
npm run seo:layouts   # 重新生成每个工具的 metadata layout
npm run build         # prebuild 会自动跑 layouts + sitemap，再静态导出到 out/
```

## 构建与部署

生产站点走 Cloudflare Workers 静态资源，**部署命令是 `npx wrangler deploy`**（不是 `wrangler pages deploy`）：

```bash
npx wrangler login
npm run deploy        # = npm run build && npx wrangler deploy
```

Cloudflare 控制台侧的配置：

| 配置项 | 值 |
| --- | --- |
| Framework preset | None |
| Build command | `npm run build` |
| Deploy command | `npx wrangler deploy` |
| Node.js version | `20` |

Canonical、Open Graph、JSON-LD、`robots.txt`、`sitemap.xml` 统一读取 `src/lib/seo.ts` 中的 `SITE_URL`（`https://calcoranow.com`）。Worker 上线后需在 Cloudflare 面板绑定 `calcoranow.com` 与 `www`。

## 项目结构

```
calculators/
├── src/app/                  # 每个分类一个目录，目录下每个工具一个 page.tsx
│   ├── page.tsx              # 首页：搜索 + 分类 + 热门工具
│   ├── all/                  # 全量目录
│   ├── finance/ …/           # 分类索引 + 各工具页面
│   └── layout.tsx
├── src/components/           # CalculatorShell、SearchableGrid、Result 等通用外壳
├── src/data/
│   ├── calculators.ts        # 工具目录（search / sitemap / all 的唯一数据源）
│   ├── seo-extras.ts         # 别名与 canonical 覆盖
│   └── tool-content.ts       # 高流量页面的正文文案
├── src/lib/                  # seo.ts（SITE_URL 等）、公式实现
├── scripts/                  # generate-tool-layouts.ts、generate-sitemap.ts
├── data/                     # 关键词调研原始数据（Keyword Planner 导出）
├── docs/                     # 设计、SEO 覆盖与内容策略
├── infra/                    # AWS CDK（旧部署方案）
└── wrangler.toml             # Cloudflare Workers 静态资源配置
```

## 新增一个计算器

一个工具要同时改到 4 个地方，缺一个就会出现"页面存在但搜不到 / 导航里没有"的情况：

1. `src/app/{category}/{slug}/page.tsx` —— 工具本体，`"use client"`，包在 `CalculatorShell` 里；
2. `src/data/calculators.ts` —— 目录条目（`title` / `description` / `href` / `icon` / `category`）；
3. `src/app/{category}/page.tsx` —— 分类网格卡片（手工维护，不从目录派生）；
4. 若是新图标，还需在 `src/components/CalculatorCard.tsx` 的 `iconMap` 中登记。

约定：结果面板在输入非法时不显示 `NaN`；公式名写在页面上（如 "reducing-balance EMI"、"Mosteller"）；可分享的输入一律走 `useHashState`；不引入 `fetch`、`localStorage` 统计或第三方挂件。加完后执行 `npm run seo:layouts`（`prebuild` 已包含）。

## 产品边界

为了保持"打开就能信"的口碑，以下内容**不做**：

- 需要实时数据的功能：实时汇率、股票/加密货币行情、WHOIS/DNS 查询、营养数据库接口；
- 需要逐年维护的税率/费率表：各国所得税、印花税、社保与公积金计划；
- 符号计算（CAS）：符号积分/求导、分步代数、LaTeX 排版求解；
- 账号体系、云端保存、服务端 PDF 生成——不为凑关键词加后端。

## License

MIT
