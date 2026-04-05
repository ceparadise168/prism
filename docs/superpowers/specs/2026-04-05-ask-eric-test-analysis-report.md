# Ask Eric — 測試分析報告

## 概要

對 ask-eric 數位分身 skill 進行了 2 輪迭代測試，使用 3 個覆蓋不同情境的測試案例，每輪包含 with-skill 和 without-skill (baseline) 的對照。

## 測試案例

| # | 情境 | 提問者角色 | 測試重點 |
|---|------|-----------|----------|
| 1 | 技術方案選擇（Polling → Event-Driven） | 同級工程師 | 多視角分析、trade-off 品質 |
| 2 | 模糊管理問題（老闆說開發太慢） | 角色不明 | 引導視角 Gate 權力 |
| 3 | Junior Code Review（SQL injection） | 新人 | 蘇格拉底模式切換 |

## Iteration 1 → Iteration 2 改進

### 修正的問題

| 問題 | Iter 1 | Iter 2 | 改善方式 |
|------|--------|--------|----------|
| Phase 結構外露 | 輸出中有 `## Phase 1：情境判斷` 等內部標籤 | 內部機制完全隱藏，直接呈現有價值內容 | 在 SKILL.md 加入「不要暴露內部流程」的明確指令 |
| 語氣過於中立 | 偏向專業建議，缺少 opinion | 有明確偏好表達（「我偏好 SQS」「不要因為 Kafka 比較專業就選 Kafka」） | 在核心身份加入語氣指導 |
| Description 觸發不足 | 描述性的，不夠 pushy | 更積極列出觸發情境 | 重寫 description |

### Iteration 2 各案例詳細比較

---

### Test Case 1：技術方案選擇

**With Skill (Iter 2) vs Without Skill (Baseline)**

| 維度 | With Skill | Baseline | 差異 |
|------|-----------|----------|------|
| 方案空間 | 4 個（加了 CDC、Webhook+Queue） | 2 個（Kafka vs SQS） | Skill 主動擴展選項 |
| 問題前置 | 先質疑「延遲太高」的標準，舉具體場景 | 直接進入比較 | Skill 先確認問題定義 |
| 表態 | 明確說「我偏好 SQS」並給理由 | 有建議但較溫和 | Skill 更有 opinion |
| 維護警告 | 專門段落談 DLQ、idempotency、schema versioning | 沒提 | Skill 多了維護視角 |
| 可觀測性 | 具體列出 4 個必須 metrics | 沒提 | Skill 多了可觀測性視角 |
| 向上溝通 | 量化 17,280 次無效 API call + elevator pitch | 沒有 | Skill 多了價值闡述視角 |
| 執行路徑 | 3 步驟（確認 webhook → PoC → 漸進切換） | 列了釐清問題但沒給具體步驟 | Skill 更 actionable |

**Iter 2 vs Iter 1 差異：** Phase 標籤消失，語氣更直接，整體讀起來像一個有經驗的工程師在對話，而非一個 AI 在做分析。

---

### Test Case 2：模糊管理問題

**With Skill (Iter 2) vs Without Skill (Baseline)**

| 維度 | With Skill | Baseline | 差異 |
|------|-----------|----------|------|
| 問題質疑 | **Gate 權力啟動** — 第一句就說「問題問錯了」 | 開頭說「先診斷」但接著給了 5 大類解法 | 根本性差異 |
| 輸出結構 | 先質疑 → 6 種根因各有具體解法 → 溝通策略 → 不受歡迎的觀點 | 列根因 → 列解法 → 溝通建議 | Skill 結構更有層次 |
| 溝通策略 | 具體教怎麼跟老闆說（帶數據、給選擇、設指標） | 有提但較簡略 | Skill 更具體 |
| 反直覺觀點 | 「也許問題不是產能低，是需求太多」 | 沒有 | Skill 敢講不受歡迎的話 |
| Eric 語氣 | 「在你衝去優化 CI/CD、推 Scrum、買 Copilot 之前」 | 較平淡的專業語氣 | Skill 語氣更直接、更有個性 |

**Iter 2 vs Iter 1 差異：**
- Iter 1：Gate 啟動後只給了診斷問題，輸出較短
- Iter 2：Gate 啟動後不只質疑問題，還展開了「假設問題是對的話」的 6 種根因分析 + 溝通策略。更完整，不會讓使用者覺得「你只是叫我回去問老闆」

這是最大的改善 — Iter 2 在行使 Gate 權力的同時，提供了足夠的實質內容，讓使用者不會空手而歸。

---

### Test Case 3：Junior Code Review

**With Skill (Iter 2) vs Without Skill (Baseline)**

| 維度 | With Skill | Baseline | 差異 |
|------|-----------|----------|------|
| 互動模式 | 純蘇格拉底 — 5 個引導問題 | 直接列 6 個問題 + 修正程式碼 | 根本性差異 |
| SQL Injection | 給具體 payload `1' OR '1'='1`，讓 Junior 自己代入 | 直接說「這是 SQL injection」 | Skill 教思考，baseline 給答案 |
| 教學效果 | 引導 Junior 自己發現：「帶入看看，你發現什麼？」 | 告訴 Junior 問題 + 給修正 | Skill 的學習效果更深 |
| 是否給修正程式碼 | 完全沒有 | 給了完整修正範例 | Skill 遵守蘇格拉底模式 |
| 結尾 | 「你覺得哪一個最想先深入聊？」 | 「有問題隨時可以再討論！」 | Skill 邀請繼續對話 |

**Iter 2 vs Iter 1 差異：** 結構更簡潔（5 個問題 vs 7 個），Phase 標籤消失，語氣更像在聊天。

---

## 核心發現

### 1. Skill 在三個維度上明確優於 Baseline

| 維度 | 描述 |
|------|------|
| **視角廣度** | Baseline 回答問題本身；Skill 先質疑問題，再從多個視角分析 |
| **互動模式切換** | Baseline 對所有人用同一種風格；Skill 對 Junior 用蘇格拉底、對同級用問答 |
| **非技術面向** | Baseline 聚焦技術；Skill 涵蓋溝通策略、向上報告、維護成本、可觀測性 |

### 2. Gate 權力是最有價值的設計

Test Case 2 完美展示了 Gate 的價值。Baseline 嘴上說「先診斷」但身體很誠實地給了一堆解法；Skill 真的把後續分析擋住了，只給診斷框架。

### 3. Iteration 2 的改善有效

| 改善項目 | 效果 |
|----------|------|
| 隱藏 Phase 結構 | 輸出從「AI 分析報告」感覺 → 「有經驗的人在跟你聊」感覺 |
| 加入語氣指導 | 「不要因為 Kafka 比較專業就選 Kafka」這種語氣出現了 |
| Gate 後仍提供實質內容 | 使用者不會覺得被打發 |

### 4. 仍存在的限制

| 限制 | 說明 |
|------|------|
| 視角派發穩定性 | 目前靠 LLM 判斷問題類型，同一問題可能被歸到不同類型。需要更多測試驗證 |
| 視角深度 vs 通用性 | 視角原則夠通用，但缺少「Eric 不會說什麼」的反模式示範，可能導致某些場景退化成通用建議 |
| Sub-agent 成本 | 完整派發多個視角的 sub-agent，token 消耗較高。需要評估是否值得 |
| 未測試的情境 | 未測試 PM/非技術角色的對話、production incident 的精簡模式、多人會議的人際互動建議 |

## 建議的後續改進

1. **加入反模式示範** — 每個視角加一段「不要這樣回答：...」的例子，避免退化成通用建議
2. **擴充測試集** — 覆蓋 PM 對話、production incident、人際互動場景
3. **視角派發穩定性測試** — 同一個問題跑 5 次，看視角選擇是否一致
4. **成本最佳化** — 測試是否可以減少 sub-agent 數量（例如合併相近視角）而不犧牲品質
5. **Description 最佳化** — 使用 skill-creator 的 run_loop 工具做觸發率測試

## 結論

Ask-eric skill 在三個測試情境中都展現了明顯優於 baseline 的表現。最大的差異不在技術深度（baseline 也能給出好的技術建議），而在**思維框架** — 先質疑問題、根據角色切換互動模式、涵蓋非技術面向。這正是 Eric 數位分身的核心價值。

Iteration 2 的改善（隱藏內部機制、加強語氣個性、Gate 後仍提供實質內容）讓輸出品質從「像 AI 分析報告」提升到「像有經驗的人在對話」。
