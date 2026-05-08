# DevTools Plus — 产品与开发计划

> 一个面向开发者的浏览器扩展工具集，集成 20+ 常用小工具（JSON、Base64、正则、时间戳、Hash 等）。
> **完全离线 · 隐私优先 · 现代 UI · 中英双语**

---

## 1. 产品定位

| 项目 | 内容 |
|---|---|
| **产品名** | DevTools Plus |
| **一句话** | 浏览器内一键调用的开发者工具集，无需切换网页 |
| **目标用户** | 前后端开发者、测试、运维、技术写作者 |
| **核心卖点** | 离线可用 · 无追踪 · 现代 UI · 划词触发 · 键盘党友好 |
| **商业模式** | 前期完全免费 + 捐赠；用户量 3 万+ 且评分 4.5+ 后引入 Pro |
| **开源协议** | MIT |

---

## 2. 竞品分析

| 产品 | 用户量 | 评分 | 定价 | 痛点 |
|---|---|---|---|---|
| DevTools for Web | ~10 万 | 4.5 | 免费 | UI 老旧，工具少 |
| Web Developer | 100 万+ | 4.4 | 免费 | 偏前端调试 |
| JSON Viewer Pro | 几十万 | 4.7 | 免费 + 捐赠 | 单一功能 |
| Smalldev.tools | 网页版 | - | 免费 + 广告 | 需打开网页 |
| DevToys (Windows) | 百万级 | - | 免费 | 仅桌面 |
| CyberChef | 高 | - | 免费 | 太复杂，学习成本高 |

### 我们的差异化
1. ✅ 浏览器内一键调用（不切窗口）
2. ✅ 划词 / 右键菜单触发
3. ✅ 快捷键支持
4. ✅ 现代 UI（Tailwind + shadcn/ui + 深色模式）
5. ✅ 历史记录（最近转换内容自动保存）
6. ✅ 完全离线（隐私敏感开发者最爱）

---

## 3. MVP 工具清单（20 个）

### 📦 数据格式
1. JSON 美化 / 压缩 / 校验 ⭐ MVP
2. JSON ↔ YAML ↔ XML ↔ TOML 互转
3. JSON Diff（两份 JSON 对比）
4. CSV ↔ JSON 互转

### 🔐 编码 / 加密
5. Base64 编解码（文本 + 图片）⭐ MVP
6. URL 编解码
7. HTML 实体编解码
8. Hash 计算（MD5 / SHA-1 / SHA-256 / SHA-512）
9. JWT 解码（Header / Payload / 签名校验）
10. UUID 生成（v1 / v4 / v7）⭐ MVP

### 🔍 文本处理
11. 正则测试器 + 可视化
12. 文本 Diff
13. 大小写转换（camel/snake/kebab/Pascal）
14. 字符串转义（JSON / SQL / Shell）

### ⏰ 时间 / 数字
15. Unix 时间戳 ↔ 日期（多时区）
16. Cron 表达式解析 + 下次执行时间
17. 进制转换（2/8/10/16 + 字节单位换算）

### 🎨 前端工具
18. 颜色转换（HEX / RGB / HSL / 取色器）
19. CSS Unit 转换（px / rem / em / vw）
20. 图片转 Base64 / SVG 压缩

### 🚀 进阶（Pro 版预留）
- Markdown 实时预览
- SQL 格式化
- Mock 数据生成
- API 调试器（轻量 Postman）
- Lorem Ipsum 生成器
- 二维码生成 / 解析

---

## 4. 技术栈

```
构建    : Vite 5 + @crxjs/vite-plugin
框架    : React 18 + TypeScript (strict)
UI      : Tailwind CSS 3 + shadcn/ui (按需引入)
图标    : lucide-react
状态    : Zustand
路由    : react-router-dom v6 (HashRouter)
i18n    : i18next + react-i18next
存储    : chrome.storage.local
Manifest: V3
包管理  : pnpm（推荐）或 npm
代码风格: ESLint + Prettier
```

❌ **禁止**：任何后端服务、任何 LLM API、任何需要网络的依赖。所有工具必须 100% 离线运行。

---

## 5. 项目结构

```
devtools-plus/
├── src/
│   ├── popup/              # 弹窗入口（点击插件图标）
│   │   ├── index.html
│   │   ├── main.tsx
│   │   └── App.tsx
│   ├── sidepanel/          # 侧边栏入口（Chrome 114+）
│   │   ├── index.html
│   │   ├── main.tsx
│   │   └── App.tsx
│   ├── options/            # 设置页
│   │   ├── index.html
│   │   ├── main.tsx
│   │   └── App.tsx
│   ├── background/         # Service Worker
│   │   └── index.ts
│   ├── content/            # 内容脚本（划词功能预留）
│   │   └── index.ts
│   ├── tools/              # 各工具实现
│   │   ├── _registry.ts    # 工具注册表（核心）
│   │   ├── json-formatter/
│   │   │   ├── index.tsx   # 工具 UI
│   │   │   ├── meta.ts     # 元数据
│   │   │   └── logic.ts    # 纯逻辑（方便测试）
│   │   ├── base64/
│   │   └── uuid/
│   ├── components/
│   │   ├── ui/             # shadcn/ui 组件
│   │   ├── ToolLayout.tsx
│   │   ├── ToolCard.tsx
│   │   ├── ThemeToggle.tsx
│   │   ├── LanguageSwitcher.tsx
│   │   └── DonateButton.tsx
│   ├── hooks/
│   │   ├── useChromeStorage.ts
│   │   ├── useTheme.ts
│   │   └── useHistory.ts
│   ├── stores/
│   │   └── settings.ts
│   ├── pages/
│   │   ├── Home.tsx        # 工具列表 + 搜索
│   │   ├── About.tsx
│   │   └── Donate.tsx
│   ├── i18n/
│   │   ├── index.ts
│   │   └── locales/
│   │       ├── en.json
│   │       └── zh-CN.json
│   ├── lib/
│   │   └── utils.ts
│   ├── styles/
│   │   └── globals.css
│   └── manifest.config.ts
├── public/
│   └── icons/ (16/32/48/128.png)
├── .github/workflows/build.yml
├── docs/
│   ├── ROADMAP.md
│   └── ADD_NEW_TOOL.md
├── LICENSE (MIT)
├── README.md
├── README.zh-CN.md
├── CONTRIBUTING.md
├── package.json
├── tsconfig.json
├── tailwind.config.ts
├── postcss.config.js
└── vite.config.ts
```

---

## 6. 品牌设计

| 项目 | 决定 |
|---|---|
| **主色调** | Indigo `#4F46E5`（Tailwind `indigo-600`） |
| **设计语感** | 参考 Linear / Raycast / Vercel |
| **Logo** | 极简 SVG，方向：`</>` + ⚡ 闪电，或扳手 + 代码符号 |
| **图标尺寸** | 16 / 32 / 48 / 128 png |
| **主题** | 深 / 浅色双主题，跟随系统默认 |

---

## 7. 三个 MVP 工具详细需求

### 7.1 JSON Formatter
- 左右两栏：左输入，右输出（支持上下布局切换）
- 按钮：**Format**（缩进 2/4 可选）/ **Minify** / **Validate**
- 校验失败时高亮错误位置
- 一键复制结果

### 7.2 Base64
- 输入框 + 编码 / 解码切换
- 文本互转
- 自动检测输入是否为合法 Base64
- 一键复制

### 7.3 UUID Generator
- 支持 **v1 / v4 / v7** 三种版本
- 批量生成：1 / 10 / 50 / 100
- 大小写切换、是否带连字符
- 一键复制全部 / 单个复制

---

## 8. 主界面（Home）

- **顶部**：搜索框（实时过滤，支持中英文 + 关键词模糊匹配）
- **工具网格**：按分类卡片展示
- **每张卡片**：图标 + 名称 + 一句话描述
- **未实现的工具**：显示在分类里，标 "Coming Soon"，不可点击
- **右上角**：主题切换 / 语言切换 / 捐赠按钮 / 设置入口

---

## 9. 捐赠页面

四个渠道：
- ☕ Buy Me a Coffee — `https://buymeacoffee.com/YOUR_HANDLE`
- 💖 Ko-fi — `https://ko-fi.com/YOUR_HANDLE`
- ⭐ GitHub Sponsors — `https://github.com/sponsors/51zhouy`
- 💰 微信 / 支付宝（占位 "Coming Soon"）

文案参考：
> "Hi, I'm an indie developer building DevTools Plus in my free time. It will always be free, ad-free, and never collect your data. If it saved you time, a coffee would mean the world to me ☕"

---

## 10. Manifest V3 配置要点

```jsonc
{
  "manifest_version": 3,
  "name": "DevTools Plus",
  "permissions": ["storage", "contextMenus", "sidePanel"],
  "action": { "default_popup": "src/popup/index.html" },
  "side_panel": { "default_path": "src/sidepanel/index.html" },
  "options_page": "src/options/index.html",
  "background": { "service_worker": "src/background/index.ts" },
  "icons": { "16": "...", "32": "...", "48": "...", "128": "..." },
  "default_locale": "en"
}
```

⚠️ **不要请求** `host_permissions`、`tabs`、`<all_urls>` 等敏感权限。

---

## 11. i18n 要求

- 至少完成 `en` 和 `zh-CN`
- 所有用户可见文案走 i18n（不要硬编码）
- 提供 `LanguageSwitcher` 组件
- 默认跟随浏览器语言

---

## 12. CI（GitHub Actions）

`.github/workflows/build.yml`：
- 触发：push 到任何分支 + PR
- 步骤：checkout → setup node 20 → install → lint → typecheck → build
- main 分支：将 `dist/` 打包为 `devtools-plus.zip` 上传 artifact

---

## 13. 开发计划（5 周到首发）

| 周 | 任务 |
|---|---|
| **Week 1** | 基础框架 + 品牌设计 + 三入口（popup/sidepanel/options） + 主题 + i18n |
| **Week 2** | 核心工具组：JSON 全套 + Base64 + URL + HTML + Hash + JWT + UUID |
| **Week 3** | 文本 + 时间工具组：正则 + Diff + 大小写 + 时间戳 + Cron + 进制 |
| **Week 4** | 前端工具组（颜色/CSS/图片） + 历史记录 + 捐赠系统 + 数据埋点 |
| **Week 5** | 性能优化 + 上架素材 + Landing Page + 隐私政策 + 三平台提交 |

---

## 14. 商业 / 收入模型

### 第一阶段：免费 + 捐赠（前 6–12 月）

| 阶段 | 时间 | 用户数 | 捐赠率 | 月捐赠 |
|---|---|---|---|---|
| 冷启动 | 1–2 月 | 500 | 0.2% | $10–30 |
| 增长期 | 3–6 月 | 5,000 | 0.2% | $50–150 |
| 稳定期 | 7–12 月 | 30,000 | 0.15% | $300–800 |

### 第二阶段：引入 Pro（满足条件后）

触发条件（任一）：
- ✅ 用户超过 30,000
- ✅ Chrome Store 评分稳定 4.5+
- ✅ 至少 3 个工具有重度用户
- ✅ 收到用户主动询问 Pro 版

切换策略：**老用户终身免费保留**，仅对新用户的高级功能收费。

| | Free | **Pro $9.99 买断** |
|---|---|---|
| 工具数量 | 15 基础 | **全部 20+** |
| 历史记录 | 5 条 | **无限 + 收藏 + 标签** |
| 主题 | 深 / 浅 | **自定义主题** |
| 数据导出 | 复制 | **批量 / 多格式** |
| 快捷键 | 默认 | **自定义** |
| 多语言 | 中 / 英 | **中 / 英 / 日** |

预计成熟期月入 **$2,000–5,000**。

---

## 15. 上架与冷启动

### 上架渠道（优先级）
1. **Chrome Web Store** ($5 一次性开发者费)
2. **Microsoft Edge Add-ons**（免费）
3. **Firefox Add-ons**（免费）
4. **Product Hunt**（首发当天）

### 冷启动获客
- 📝 技术博客：dev.to / Medium / 掘金 / 知乎
- 🐦 Twitter / 小红书：build in public
- 🌐 Reddit：r/webdev、r/programming、r/SideProject
- 🎯 Hacker News：Show HN
- 💬 Indie Hackers：发布故事
- 📺 YouTube / B站：30 秒功能演示
- 📚 GitHub Awesome Lists：提 PR 加入 awesome-chrome-extensions

### Landing Page 必备
- Hero：一句话价值主张 + 演示 GIF
- 工具列表（带图）
- "为什么不用网页版" 对比
- 隐私承诺（"100% 离线 / 零追踪"）
- 定价（Free vs Pro 占位）
- 用户评价（早期找朋友刷 5 星）

---

## 16. 捐赠转化技巧

让 0.2% → 0.5% 的关键：

1. **「成功瞬间」触发**：用户成功格式化超长 JSON 后，弹一个轻提示「✨ Helped you save 10 seconds! [Buy me a coffee ☕]」
2. **About 页面讲故事**：独立开发者口吻，强调"永远免费、无广告、不收集数据"
3. **设置页常驻入口**：左下角小图标，不打扰
4. **里程碑庆祝**：「🎉 You've used DevTools Plus 100 times!」
5. **开源 + GitHub Stars**：信任度提升 3–5 倍

---

## 17. 验收标准

- [ ] `pnpm install && pnpm dev` 能启动开发服务器
- [ ] `pnpm build` 产出 `dist/`，可作为 unpacked extension 加载到 Chrome
- [ ] popup 正常打开，能看到工具列表，3 个工具能正常使用
- [ ] 深 / 浅主题切换正常
- [ ] 中英文切换正常
- [ ] 捐赠页面正常显示
- [ ] CI 通过
- [ ] README 完整、清晰、专业

---

## 18. 风险与应对

| 风险 | 概率 | 应对 |
|---|---|---|
| 竞品太多，没人下载 | 高 | 主打"离线 + 现代 UI + 划词触发"差异化 |
| Free 用户不付费 | 高 | Pro 功能要"高频用户必需"，不是装饰 |
| Chrome Store 审核被拒 | 中 | 严格遵守 Manifest V3，无可疑权限 |
| 评分被恶意拉低 | 中 | 早期主动收集反馈，快速响应 Bug |
| 功能太多反而臃肿 | 中 | MVP 只做 15 个，慢慢加 |

---

## 19. 启动成本

| 项目 | 费用 |
|---|---|
| Chrome Web Store 开发者注册 | $5（一次性） |
| 域名 | $10/年 |
| 托管（Cloudflare Pages） | 免费 |
| Lemon Squeezy 收款 | 5% 抽成（仅在���钱时） |
| Logo 设计（自己用 Figma） | 免费 |
| **总计** | **~$15** |

---

## 20. 不要做的事

- ❌ 不要接任何 LLM / 在线 API
- ❌ 不要写后端代码
- ❌ 不要请求过多浏览器权限
- ❌ 不要做"假"工具（有 UI 没功能）—— 要么完整做，要么 "Coming Soon" 不可点击
- ❌ 不要引入太重的 UI 库（Ant Design / MUI），坚持 Tailwind + shadcn/ui
- ❌ 不要硬编码用户可见文案，必须走 i18n

---

## 附录 A：成功指标（KPI）

| 时间节点 | 目标 |
|---|---|
| 上架第 1 周 | 100 安装 |
| 上架第 1 月 | 1,000 安装 · 4.5+ 评分 |
| 上架第 3 月 | 5,000 安装 · 首批捐赠 |
| 上架第 6 月 | 20,000 安装 · 月捐赠 $100+ |
| 上架第 12 月 | 50,000 安装 · 月捐赠 $300+（或 Pro 化后 $2,000+） |

---

## 附录 B：参考的成功独立开发者案例

| 产品 | 类型 | 收入 |
|---|---|---|
| Octotree | GitHub 代码树 | 月入 $50k+ |
| Keepa | 亚马逊比价 | 年入千万美元 |
| Momentum | 新标签页 | 千万用户级 |
| DF Tube | YouTube 净化 | 50 万+ 用户 |
| JSON Viewer Pro | JSON 美化 | 几十万用户 |

**共同点**：纯前端 · 功能极其专注 · 长期运营。

---

_本文档由产品规划阶段输出，可根据开发进展持续更新。_
