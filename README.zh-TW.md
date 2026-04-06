# Prism

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Version](https://img.shields.io/github/v/tag/ceparadise168/prism?label=version)](https://github.com/ceparadise168/prism/releases)

**[English](README.md)**

一個問題進去，多重視角出來。

Prism 是一個將工程師思考方式編碼成可重用 AI skill 的框架。它不儲存知識——它捕捉的是**一個人怎麼思考**：怎麼質疑問題、考慮哪些面向、什麼時候會推回去、以及如何針對不同對象調整溝通方式。

## 為什麼需要 Prism

當一個資深工程師離開團隊，程式碼會留下，但判斷力會跟著走。Prism 將這些判斷力捕捉為結構化的思維框架，讓 AI 可以執行。

## 運作方式

```
使用者提問
       |
       v
  引導視角（gate power）
  「這個問題問對了嗎？」
       |
       +-- 需要重構問題 --> 要求使用者重新思考
       +-- 不需要技術方案 --> 非技術建議
       +-- 確認 --> 繼續
       |
       v
  派發相關視角（並行分析）
  [架構] [品質] [安全] [務實] [...]
       |
       v
  根據互動模式彙整
  （蘇格拉底式 / Q&A / Review / 精簡）
       |
       v
  多視角回應
```

關鍵設計決策：
- **引導視角擁有 gate power** — 如果問題本身需要重構，它可以短路所有分析
- **互動模式隨對象調整** — 對 junior 用蘇格拉底式，對 peer 用 Q&A，對 PM 去技術化
- **每個視角都有反模式** — 每個視角都知道「通用 AI 建議」長什麼樣，然後避開它

## 輸出範例

<details>
<summary><b>同事問：「Kafka 還是 SQS？」</b></summary>

> 輸入：「我們的即時累點系統現在用 polling 每 5 秒去撈一次 CRM API，延遲太高了，想改成 event-driven。目前有在考慮用 Kafka 或是 AWS SQS，你覺得呢？」

**沒有 Prism** — Claude 比較 Kafka vs SQS，給出平衡的優缺點清單，建議「取決於你的需求」。

**有 Prism** — skill 會：
1. **先質疑前提**：「你說延遲太高，高到什麼程度算問題？5 秒在 App 顯示點數 vs 5 秒內推播通知，嚴重程度差很多」
2. **擴展選項空間**：加入 Webhook+Queue、EventBridge、Database CDC、polling 優化——不只是使用者提到的兩個選項
3. **表明偏好**：「我偏好 SQS。不要因為 Kafka 比較專業就選 Kafka。」——附上團隊能力和維運負擔的具體理由
4. **警告隱藏成本**：DLQ、冪等性、schema versioning、以及「event-driven 的 debugging 難度會上升」
5. **給出利害關係人簡報**：「17,280 次無效 API call/天 → 降到實際事件數量」

</details>

<details>
<summary><b>有人問：「老闆覺得我們太慢，怎麼辦？」</b></summary>

> 輸入：「老闆覺得我們的開發速度太慢了，要我想辦法加速，你覺得該怎麼辦？」

**沒有 Prism** — Claude 說「先診斷根本原因」然後馬上列出 5 類解法（需求、技術債、流程、規劃、工具）。

**有 Prism** — 引導視角**啟動 gate power**：

> 「等一下。在你衝去優化 CI/CD、推 Scrum、買 Copilot 之前，我想先質疑這個問題本身。『開發速度太慢』這句話，問題問錯了。這是一個症狀描述，不是問題定義。」

Skill 拒絕給解法，直到使用者回答：「慢」是什麼意思？怎麼測量的？跟什麼比？然後給出具體第一步：「Make Work Visible — 追蹤最近 3-5 個 feature 的生命週期，找出時間花在哪裡。」

</details>

<details>
<summary><b>Junior 請求 code review（蘇格拉底模式）</b></summary>

> 輸入：一位 junior 工程師分享他的第一支 API endpoint（有 SQL injection、缺少驗證、錯誤的 null check）

**沒有 Prism** — Claude 列出全部 6 個問題，提供修正後的程式碼，說「有問題隨時可以再討論！」

**有 Prism** — 自動切換到蘇格拉底模式。不列問題，而是提問：

> 「如果有人傳這個進來，會發生什麼？」
> ```
> memberId: "1' OR '1'='1"
> ```
> 「把它帶入你的 SQL 字串，看看組出來的 query 長什麼樣子。你發現什麼了嗎？」

沒有修正後的程式碼。沒有直接答案。5 個引導問題讓 junior 自己發現每個問題。最後：「你覺得哪個問題最值得先深入？」

</details>

<details>
<summary><b>Tech Lead 面對人際 + 技術衝突</b></summary>

> 輸入：「Senior 堅持用 MongoDB 做訂單系統，但我覺得 PostgreSQL 比較適合。他資歷比我深，每次開會提反對意見他就不太高興。」

**沒有 Prism** — Claude 給技術比較 + 通用建議「建議保持專業、開放溝通、用數據說話」

**有 Prism** — 重構問題並模擬 Senior 的反應：

> 「你真正的問題不是 MongoDB vs PostgreSQL，是怎麼在資歷壓制的環境裡推動正確的技術決策。」
>
> 「如果我是那個 Senior，有人說『我覺得 PostgreSQL 比較適合』，我的第一個反應不是『他說的對不對』，而是『他是在挑戰我，還是在貢獻討論？』」

給出具體行動計畫：寫一頁技術分析，在開會前私下分享，把框架設定為「我想聽你對這幾個疑問的看法」而不是「我反對」。

跨視角共識：「你的問題是你的論點不夠強，而不是你說話的機會不夠多。先武裝自己，再選擇戰場。」

</details>

## 20 個視角，8 個層次

| 層次 | 視角 | 核心問題 |
|------|------|----------|
| 問題定義 | 引導、使用者故事 | 問題問對了嗎？ |
| 方案探索 | 研究 | 有哪些選項？ |
| 技術深度 | 根因、架構、品質、安全、開發方法論、維護 | 怎麼做才對？ |
| 系統運行 | 可觀測性、事故應對 | 看得到嗎？壞了怎麼辦？ |
| 變更執行 | 變更執行 | 相依性、回滾、驗證、通知？ |
| 系統價值 | 數據、營運、客戶體驗 | 能形成飛輪嗎？ |
| 落地與推動 | 務實、專案管理、價值闡述、人際互動 | 能上線嗎？能拿到支持嗎？ |
| 永續經營 | 治理 | 能長期運作和成長嗎？ |

## 快速開始

### 搭配 Claude Code 使用（Plugin）

**第一步 — 加入 marketplace：**

```
/plugin marketplace add ceparadise168/prism
```

**第二步 — 安裝 plugin：**

```
/plugin install prism@ceparadise168-prism
```

完成。輸入 `/` 就能看到 `prism:ask-eric`：

```
/prism:ask-eric 我們打算把 monolith 拆成 microservices，團隊只有 5 個人，你怎麼看？
```

**管理 plugin：**

| 操作 | 指令 |
|------|------|
| 更新到最新版 | `/plugin update prism` |
| 暫時停用 | `/plugin disable prism` |
| 重新啟用 | `/plugin enable prism` |
| 移除 | `/plugin uninstall prism` |
| 查看狀態 | `/plugin`（開啟 plugin 管理介面） |

**與團隊共用** — 加到專案的 `.claude/settings.json`：

```json
{
  "extraKnownMarketplaces": {
    "ceparadise168-prism": {
      "source": { "source": "github", "repo": "ceparadise168/prism" }
    }
  },
  "enabledPlugins": {
    "prism@ceparadise168-prism": true
  }
}
```

團隊成員開啟專案時會自動收到安裝提示。

**本地測試（給貢獻者）：**

```bash
git clone https://github.com/ceparadise168/prism.git
claude --plugin-dir ./prism
```

本地載入的 plugin 用 `@` 呼叫：

```
@ask-eric/ 你的問題
@ask-founder/ 你的問題
```

注意：本地載入用 `@skill-name/` 語法，不是 `/plugin:skill-name`。

### 搭配其他 LLM 使用（ChatGPT、Gemini 等）

將 [`eric-engineering-mind.md`](eric-engineering-mind.md) 的內容複製到你的 LLM 系統提示中，或在對話開頭貼上。然後直接提問即可——不需要 slash command。

### 建立你自己的 Prism

參見 [CONTRIBUTING.md](CONTRIBUTING.md) 的逐步指南。

## 範例：`ask-eric`

`plugins/prism/skills/ask-eric/` 目錄是一個完整的 Prism 實例——Eric 工程思維的數位分身。它展示了全部 20 個視角，包含 Eric 特有的原則、反模式和語氣。

```
/prism:ask-eric 我們打算把 monolith 拆成 microservices，團隊只有 5 個人，你怎麼看？
```

Skill 會：
1. 質疑 5 個人能不能撐住 microservices（引導視角）
2. 分析架構上的 trade-offs（架構視角）
3. 用團隊脈絡挑戰前提（務實視角）
4. 警告維運複雜度（營運視角）
5. 彙整成有觀點、有具體建議的回應

## 通用版本

`eric-engineering-mind.md` 是獨立的 Markdown 檔案，包含相同的思維框架，不依賴 Claude Code。可以餵給任何 LLM 作為系統提示。

## 專案結構

```
prism/
├── .claude-plugin/
│   └── marketplace.json           # Marketplace 定義
├── plugins/
│   └── prism/
│       ├── .claude-plugin/
│       │   └── plugin.json        # Plugin manifest
│       └── skills/
│           ├── ask-eric/          # 工程判斷力 skill
│           │   ├── SKILL.md       # 協調器（人格 + 派發 + 彙整）
│           │   ├── perspectives/  # 20 個視角檔案
│           │   └── README.md      # Skill 使用說明
│           └── ask-founder/       # 創業判斷力 skill
│               ├── SKILL.md       # 協調器（人格 + 派發 + 彙整）
│               └── perspectives/  # 12 個視角檔案
├── eric-engineering-mind.md       # 通用版本（任何 LLM）
├── docs/                          # 設計文件與測試報告
├── LICENSE                        # MIT
├── README.md                      # 英文版
└── README.zh-TW.md               # 本檔案（繁體中文）
```

## 授權

MIT
