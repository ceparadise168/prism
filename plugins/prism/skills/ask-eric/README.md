# Ask Eric — 數位分身 Skill

Eric 的工程思維數位分身。不是知識庫，是思維框架。

## 安裝

### Claude Code（Plugin 方式）

```
/plugin marketplace add ceparadise168/prism
/plugin install prism@ceparadise168-prism
```

安裝完成後，輸入 `/` 就能看到 `prism:ask-eric`。

**管理：**

| 操作 | 指令 |
|------|------|
| 更新 | `/plugin update prism` |
| 停用 | `/plugin disable prism` |
| 啟用 | `/plugin enable prism` |
| 移除 | `/plugin uninstall prism` |
| 狀態 | `/plugin` |

## 使用

```
/prism:ask-eric 我們的 API response time 最近變很慢，要怎麼處理？
```

```
/prism:ask-eric [貼上 code] 幫我 review 一下
```

```
/prism:ask-eric 老闆想要加一個即時通知功能，你覺得呢？
```

## 它會做什麼

1. **判斷情境** — 你的角色、問題類型、緊急程度
2. **先質疑問題** — 引導視角先行，確認問題問對了
3. **多視角分析** — 派出相關視角的 sub-agent 並行分析
4. **彙整觀點** — 呈現各視角的觀察和 trade-offs

## 它不會做什麼

- 不涉及公司機密商業邏輯
- 不替你做決策 — 呈現 trade-offs，你自己選
- 不用權威語氣 — 不說「Eric 說要這樣做」

## 20 個視角

| 層次 | 視角 |
|------|------|
| 問題定義 | 引導、使用者故事 |
| 方案探索 | 研究 |
| 技術深度 | 根因、架構、品質、安全、開發方法論、維護 |
| 系統運行 | 可觀測性、事故應對 |
| 變更執行 | 變更執行 |
| 系統價值 | 數據、營運、客戶體驗 |
| 落地與推動 | 務實、專案管理、價值闡述、人際互動 |
| 永續經營 | 治理 |

## 非 Claude Code 使用

如果你使用其他 LLM（ChatGPT、Gemini 等），請使用 repo 根目錄的 `eric-engineering-mind.md`。這份檔案包含相同的思維框架，純 Markdown 格式，任何 LLM 都能用。
