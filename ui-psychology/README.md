# 🧠 UI Psychology Skill for Claude

> 用心理學框架驅動每一個設計決策——不只讓介面「好看」，而是讓用戶「忍不住行動」。

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Claude Skill](https://img.shields.io/badge/Claude-Skill-blueviolet)](https://claude.ai)

---

## 這是什麼？

這是一個 **Claude Skill**，讓 Claude 在回答 UI/UX 問題時，能以系統化的心理學框架分析、設計、並審查介面。

裝上這個 Skill 之後，你可以對 Claude 說：
- 「幫我分析這個 Landing Page 為什麼轉換率低」
- 「設計一個符合心理學的 SaaS 註冊流程」
- 「從零生成一個定價頁的設計規格」
- 「全面審查我的 Onboarding 流程」

Claude 會輸出結構化的分析報告、User Flow 設計文件、元件規格，以及 HTML/React 互動原型。

---

## 核心框架：三層心理學模型

```
👁️ 感知層（Perception）  →  用戶「看到」什麼？
🧠 認知層（Cognition）   →  用戶「理解」什麼？需要花多少腦力？
🎯 行為層（Behavior）    →  什麼「驅動」或「阻礙」用戶行動？
```

內建 20+ 心理學原則，包括：
損失規避 · 錨定效應 · Hick's Law · Zeigarnik Effect · 社會認同 · 峰終定律 · PACE Framework · BJ Fogg 行為模型 ...

---

## 四種操作模式

| 模式 | 觸發語句範例 | 輸出 |
|------|------------|------|
| **ANALYZE** 分析 | 「這個 UI 為什麼沒人點？」| 三層評分 + 問題診斷 + ROI 修改清單 |
| **USERFLOW** 流程設計 | 「設計一個符合心理學的購買流程」| 心理旅程地圖 + 步驟規格 + 互動原型 |
| **GENERATE** 生成 | 「幫我生成定價頁設計規格」| 元件清單 + 文案框架 + 視覺規格 |
| **AUDIT** 審查 | 「全面審查我的 Onboarding」| 85 項清單評分 + 嚴重性矩陣 + 優化路線圖 |

---

## 文件結構

```
ui-psychology/
├── SKILL.md                      # 主入口：模式決策 + 框架 + 輸出模板
└── references/
    ├── principles.md             # 20+ 心理學原則完整庫（含研究數據）
    ├── userflow.md               # PACE 框架 + 5 種 Flow 類型策略 + 旅程地圖模板
    ├── patterns.md               # UI Pattern × 心理學對應表
    └── audit-checklist.md       # 85 個系統性審查項目
```

---

## 安裝方式

### 方法一：下載 `.skill` 檔案
1. 從 [Releases](../../releases) 下載 `ui-psychology.skill`
2. 在 Claude.ai 的 Settings → Skills 上傳

### 方法二：手動安裝
1. Clone 這個 repo
2. 將 `ui-psychology/` 資料夾上傳至 Claude Skills

---

## 輸出範例

### USERFLOW 輸出片段

```markdown
## 步驟 2：填寫 Email

**用戶心理狀態**：「我為什麼要給你我的 Email？會被垃圾郵件嗎？」
**心理學策略**：互惠原則 + 信任建立 — 先給用戶明確好處，再請求資料

| 元件 | 內容 | 心理學根據 | 優先級 |
|------|------|-----------|:-----:|
| 標題 | `免費獲得你的個人化報告` | 互惠原則 | P0 |
| Email 欄位 | Floating label，即時驗證 | 認知負荷↓ | P0 |
| 隱私說明 | `我們不會發垃圾郵件，隨時可取消訂閱` | 信任建立 | P1 |
| CTA | `立即獲取報告 →` | 結果導向動詞 | P0 |
```

### AUDIT 輸出片段

```markdown
### 🎯 嚴重性矩陣
| 問題 | 嚴重度 | 修改難度 | 優先分數 |
|------|:-----:|:------:|:-------:|
| CTA 文字用「提交」（無意義動詞）| 5 | 1 | 10.0 |
| 定價頁有 5 個方案（Hick's Law 違反）| 4 | 3 | 2.67 |
| 沒有退款保證說明 | 4 | 1 | 8.0 |
```

---

## 設計原則

這個 Skill 的每一個輸出都遵守：

1. **永遠說明心理學根據** — 不只告訴你「要這樣做」，要解釋「因為 XX 原則，用戶會 XX 反應」
2. **量化預期效果** — 給出研究數據或預期轉換率變化
3. **ROI 優先排序** — 永遠告訴你「先做哪個」
4. **具體到可執行** — 每個建議具體到「把 XX 改成 XX」
5. **Markdown 主導** — 主文件自給自足；HTML/React 原型作為輔助

---

## 心理學原則速查

| 原則 | 核心概念 | 設計應用 |
|------|---------|---------|
| 損失規避 | 失去的痛苦是收穫的 2 倍 | 「你將失去...」> 「你將獲得...」|
| 錨定效應 | 第一個數字決定判斷基準 | 先展示高價，再展示目標價 |
| Hick's Law | 選項越多，決策越慢 | 選項控制在 7 以內 |
| 社會認同 | 不確定時，模仿他人 | 帶頭像的真實評論 + 用戶數 |
| Zeigarnik Effect | 未完成的任務更有拉力 | 進度條 + 完成度顯示 |
| 峰終定律 | 記憶由峰值與終點決定 | 精心設計 Aha Moment 和成功頁 |
| PACE Framework | Pain×Anxiety×Confidence×Energy | 每個步驟分析用戶心理四維度 |

完整原則庫（含研究數據）：[references/principles.md](./references/principles.md)

---

## License

MIT — 歡迎 fork、修改、分享，標注來源即可。

---

*Built with ❤️ by Jason Tsai · 如果對你有幫助，歡迎 ⭐ 這個 repo*
