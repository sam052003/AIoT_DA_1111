# AirGuard 專題提案解析.pdf｜文字備份

> 此檔為原始「AirGuard 專題提案解析.pdf」的**自動抽取文字備份**，僅供 GitHub 搜尋與檢閱。圖表、版面、圖片與表格格式可能未完整保留；原始檔仍應以 DOCX／PPTX／PDF 為準。提案階段，非實作驗證成果。

---

```text
<PARSED TEXT FOR PAGE: 1 / 4>

依據筆記本中的**《期末專題提案作業規範》與《A2Z outline 論文架構 SOP》**標準，對
AirGuard_AI_Final_Proposal.docx（正式書面提案報告書）與
AirGuard_AI_Final_Proposal_Presentation.pptx（24 頁提案簡報）進行詳細的結構、技術與
規範落實度解析 1-4。
一、 總體規範符合度評估（Executive Alignment）
《期末專題提案作業規範》的核心原則為：
\\[\text{Domain AI Agent} + \text{Domain Knowledge} + \text{Data Analytics} +
\text{Real-World Application} \text{ 5}\\]
拒絕「只訓練單一 AI 模型」或「純聊天 Chatbot」6。檢視 DOCX 與 PPTX 的設計，兩者高度
一致且全面落實此精神 2, 3：
  1.​ Real-World Application：鎖定真實戶外活動（如慢跑、通勤、敏感族群防護）決策支
        援，而非空泛的空品展示 2, 3, 7, 8。
  2.​ Data Analytics：介接環境部開放資料（AQX_P_13 逐時歷史值、AQX_P_432 即時
        AQI），設計防時序洩漏（Rolling-origin、70/15/15 切分）的 1、3、6 小時
        \\(\text{PM}_{2.5}\\) 預測 9-14。
  3.​ Domain Knowledge：導入 2025 年新版環境部 AQI 分級與活動副指標指引，落實
        「官方已發布 AQI」與「模型預測 \\(\text{PM}_{2.5}\\)」分流之雙軌防護機制 10, 13,
        15-17。
  4.​ Domain AI Agent：基於 ReAct 模式受控工具呼叫（Tool Allowlist），負責自然語言情
        境解析、證據彙整、不確定性約束與安全降級，嚴禁 LLM 捏造數值或給予個人醫
        療診斷 8, 9, 15, 18, 19。
二、 對照《期末專題提案作業規範》七大維度解析

1. 摘要與緒論標準（Abstract A–F & Introduction）
    ●​ A–F 六段式研究故事：DOCX 摘要與 PPTX 第 5 頁嚴格對齊規範 2, 7, 9, 20：
    ●​ A (Attention Getter)：引用 2024 WHO 全球室外空污致 420 萬人早逝數據，搭配
       2026 環境部公布之 2025 年臺灣 \\(\text{PM}_{2.5}\\) 年均值 \\(12.8\
       \mu\text{g/m}^3\\) 2, 7, 21。
    ●​ B (But)：指出既有資訊僅展示現況，缺乏行動決策轉譯；ML 時序模型易發生時序
       洩漏 9, 20。
    ●​ C (Cure)：提出「AirGuard AI：智慧空氣品質預測與生活決策代理人」9, 20。
    ●​ D (Development)：整合環境部 API/CSV、Persistence/Ridge/RF/XGBoost 預測與官方
       活動指引 9, 20。
    ●​ E (Experiments)：時序滾動切分回測（MAE、RMSE、Skill Score）與 30 個 Agent 情境
       驗收 9, 20。
    ●​ F (Findings - Expected Outcomes)：恪守規範「Proposal 階段不得虛構實驗成果」，
       清楚標示為預期產出（Expected Outcomes） 7, 20, 22。
    ●​ 評分占比對應：符合規範緒論 20% 要求（具體數據引題、問題定義清晰、差異化創
       新明確）23, 24。

2. 文獻研究與 4x5 彙整表（Related Work 1/2 AI + 1/2 Domain）
    ●​ AI Technology 與 Domain Know-how 均衡性：DOCX 第 2 節與 PPTX 第 7–9 頁平衡
       探討預測模型（Chianese 2026、Joseph 2025）、可解釋性（Houdou 2024）、Agent 調
       度（ReAct 2023、Nie 2025）及環境領域知識（WHO 2021/2024、臺灣環境部
       2025/2026）8, 16, 17, 25, 26。
    ●​ Article Summary Table：
    ●​ DOCX 第 2.5 節提供完整 8 欄對照表（Ref, Year, Problem, AI Method, Domain
       Knowledge, Dataset, Findings, Limitation）收錄 10 篇精選文獻；PPTX 第 9 頁則摘要

<PARSED TEXT FOR PAGE: 2 / 4>

      關鍵 6 篇 27-30。
   ●​ 四階段邏輯鏈歸納：DOCX 第 2.4 節與 PPTX 第 10 頁完整呈現 Existing Research →
      Limitations → Research Gap → Our Project，明確指出研究缺口為「臺灣測站尺度
      下，結合短期預測、官方活動指引與可追溯 Agent 在資料不完整時的決策可靠性
      驗證」27, 31, 32。

3. Deep Research：三大核心問題（專門章節檢視）
符合規範 20% 權重之要求，深入剖析領域本質 24, 33-38：
    ●​ Q1. 5 個核心思維模式（Mindsets）（DOCX 3.1 / PPTX 11）28, 31, 39, 40：
    ●​ Exposure over visualization：決策導向而非單純圖表展示。
    ●​ Spatiotemporal fidelity：時空、測站、時間戳與平均窗嚴格一致。
    ●​ Baseline-first and leakage-safe：堅持 Persistence 基線與防洩漏切分。
    ●​ Explain without overclaim：SHAP 僅作特徵關聯解釋，絕不擅作因果推論。
    ●​ Human-centered, fail-safe agent：人本導向，遇異常寧可承認未知安全降級。
    ●​ Q2. 3 個關鍵爭論（Controversies）（DOCX 3.2 / PPTX 12）39-42：
    ●​ 模型複雜度（Deep Learning/GNN vs. Persistence/Tree Models）：共識為無通用最佳
       模型，極短期時序需依回測取捨。
    ●​ 準確預測 vs. 可解釋與安全（追求低 RMSE vs. 來源追溯與規則一致）：共識為兩者
       皆需驗證，非專家決策更重信任度。
    ●​ Agent 自主程度（完全自主 vs. 規則約束）：共識為環境決策中的 LLM 應採受限輔
       助與規則防護。
    ●​ Q3. 10 個深度理解問題（DOCX 3.3 / PPTX 13）41, 42：
    ●​ 涵蓋 Why、What-if、Trade-off、Failure Case、Evidence、Comparison、Design Decision
       、Real-world Scenario、Uncertainty、Causality 十大維度，並附有深入評判要點 41,
       42。

4. 系統設計與三大技術表示（Proposed Scheme）
    ●​ 八大模組架構（System Architecture ①–⑧）：DOCX 第 4.2 節與 PPTX 第 15 頁精確
       對齊規範推薦之 8 個模組編號 10, 18, 19, 43-45：
    ●​ ① User/Web UI \\(\rightarrow\\) ② Query Interpreter \\(\rightarrow\\) ③ Planner
       Agent \\(\rightarrow\\) ④ Data Acquisition \\(\rightarrow\\) ⑤ Analytics Engine
       \\(\rightarrow\\) ⑥ Domain Rules \\(\rightarrow\\) ⑦ Decision Engine
       \\(\rightarrow\\) ⑧ Output & Interaction。
    ●​ 流程圖（Flowchart）：DOCX 第 4.3 節與 PPTX 第 16 頁繪出資料品質檢驗、時距檢核
       及非即時安全降級路徑（Quality Check = NO 時降級，不捏造數值）10, 13, 19, 45。
    ●​ 演算法偽程式碼（Pseudocode）：
    ●​ DOCX 完整提供雙演算法：Algorithm 1 (AirGuardAgent) 21 行具行號核心 Agent 調
       度程序（含工具白名單、數值/時間/規則守門、審計日誌）11, 46, 47；Algorithm 2
       (TrainAndEvaluate) 17 行時序防洩漏訓練驗證程序 47-49。
    ●​ PPTX 第 19 頁則收錄核心 20 行 Agent 調度與雙軌驗證偽程式碼 14, 50, 51。

5. 評估設計與雙軌驗證（Experiments & Evaluation）
DOCX 第 5 節與 PPTX 第 20 頁設計了嚴密的雙軌評估機制（Dual-track Evaluation） 12,
51-53：
    ●​ Track A (ML 預測)：1/3/6 小時時距，以 Persistence 與 Seasonal Naive 為 Benchmark
       ，評估 Ridge、RF、XGBoost 之 MAE、RMSE 與 Skill Score，採用 70/15/15 滾動起點（
       Rolling-origin）驗證 12, 51, 52。

<PARSED TEXT FOR PAGE: 3 / 4>

   ●​ Track B (Agent 決策)：建立至少 30 個固定邊界測試案例（測站歧義、資料延遲、超
      時距、混淆 AQI、敏感族群），量化評估「工具選擇正確率」、「來源完整率」、「規則
      一致率」與「安全降級率」12, 51-53。

6. 專案規劃與風險控制（Roadmap & Risks）
    ●​ W1–W6 交付路線：由資料盤點 (W1)、基線回測 (W2)、Agent 工具 (W3)、Web 介面
       (W4)、雙軌實驗 (W5) 至最終成果交接 (W6) 53-55。
    ●​ 風險與緩解矩陣：涵蓋 API 延遲快取、模型未勝基線時降階為趨勢分析、防止 LLM
       幻覺與明確標記「測站尺度」（不跨足街道微環境個人暴露與醫療診斷）53, 54。
三、 對照《A2Z outline 論文架構 SOP》結構拆解
AirGuard_AI_Final_Proposal.docx 在各章節佈局上，完美映射了學術論文的 A–Z 字母模組
化節奏 1, 2：
A2Z 階段,A2Z 模組代號與定義,DOCX 與 PPTX 內容落實點
Abstract,"A–F (Attention, But, Cure, Development, Experiments, Findings) 1","摘要完全採
A–F 小標題結構；Findings 明確定義為 Expected Outcomes，不捏造實驗 2, 7, 9, 20。"
I. Introduction,"G–L (General 現況, However 挑戰, In literature 文獻解, Judgement 評論,
Keypoint 創新, List 組織) 1","第 1.1–1.6 節由 WHO/環境部數據 (G) 展開，指出行動轉譯痛
點 (H)，評論既有模型 (I/J)，提出雙軌防護與可解釋決策創新 (K)，並條列預期貢獻與組織
(L) 7, 15, 25。"
II. Related Work,"M–O (Methods 現有方法, New proposed 新穎性, Organize 歸納 4x5 表)
1","第 2.1–2.2 節區分 AI 技術與領域知識 (M)；第 2.4 節四階段歸納 Research Gap 與新方
法 (N)；第 2.5 節提供完整 Article Summary Table (O) 16, 25, 27, 28。"
III. Proposed Scheme,"PA–PM (Aim 目標, Background 背景, Cure 解法,
Design/Elements/Graph/How/Implementation/Jump-example/Proof) 1","第 4 節完整包含
研究目標 (PA)、環境部資料背景 (PB)、雙軌架構解法 (PC)、8 模組圖與資料契約 (PD–PG)
、21 行 Algorithm 1 偽程式碼與資料流 (PH/PI)，以及 S1–S3 慢跑/敏感族群生活範例 (PJ)
10, 11, 18, 46, 47。"
IV. Simulation,"Q–V (Quality/Quantity 指標, Related methods 基線, Setup 設定, Tuning 調
校, Useful results, Verify 驗證) 1","第 5 節列出 MAE/RMSE/Skill (Q)；Persistence/Seasonal
Naive 基線對比 (R)；臺中測站 70/15/15 Rolling-origin 設定 (S)；消融實驗與不確定性區間
校準 (T)；預期成果與 30 個測試情境驗證 (U/V) 12, 52。"
V. Conclusion,"W–Z (What proposed 回顧, eXcel 專精領域, Yields 預期產出, Zen 限制與展
望) 1","第 5.4 與第 6 節回顧決策支援定位 (W)；專精於測站尺度短期活動建議 (X)；條列
四大交付物 DOCX、PPTX、GitHub、DESIGN.md (Y)；坦承街道空間尺度局限與非醫療診斷
限制 (Z) 52, 54-56。"
四、 DOCX 與 PPTX 之一致性與差異互補檢視
   ●​ 核心概念與名詞高度一致：
   ●​ 專案名稱、研究定位（Domain AI Agent × Open Data × PM2.5 Forecasting ×
      Explainable Decision Support）在書面報告與 24 頁簡報完全對齊 2, 3。
   ●​ 模組編號 ①–⑧、三項數據集代碼（AQX_P_432、AQX_P_488、AQX_P_13）、三個核
      心使用情境（S1 慢跑、S2 敏感族群、S3 異常降級）完全吻合 8, 10, 11, 13, 18, 19,
      43, 57。
   ●​ 呈現形式的互補性：
   ●​ DOCX 著重嚴謹度與細節：完整收錄 10 篇文獻的 Article Summary Table、Deep
      Research 10 大問題的具體判別要點、Algorithm 1 與 Algorithm 2 的詳細行號與資
      料型態定義 11, 27, 28, 41, 46-49。
   ●​ PPTX 著重視覺化與傳達力：頁數達 24 頁（符合作業規範 >20 頁要求 58），將複雜
      的流程提煉為清楚的 Slide 卡片（如第 15 頁架構圖、第 16 頁狀態流程圖、第 20

<PARSED TEXT FOR PAGE: 4 / 4>

       頁雙軌評估對照圖），並在第 21–23 頁凸顯可重現交付與限制宣告 19, 43, 51, 53,
       55, 56。
五、 結論與口頭審查準備建議
AirGuard AI 的提案文件（DOCX 與 PPTX）是標準且極具深度的期末專題提案典範。它完全
避免了「單純套用 API 做 Chatbot」或「盲目訓練深度學習模型卻無基線對照」的常見缺陷
，將專業環境領域法規（AQI 副指標、時間平均窗）深度固化於系統邊界中 6, 15, 16, 39。
後續口試或評審時建議聚焦的防守重點：
  1.​ 為什麼不直接預測未來 AQI？ 需能流暢回答：AQI 是包含 6 種污染物（
       \\(\text{O}3, \text{PM}{2.5}, \text{PM}_{10}, \text{CO}, \text{SO}_2, \text{NO}2\\)）
       且採不同時間移動平均計算出的綜合指標；本系統只預測 \\(\text{PM}{2.5}\\) 單
       一濃度，絕不擅自捏造「未來的官方 AQI」，故採雙軌並行 3, 15, 16, 41。
  2.​ 若 XGBoost 預測表現沒有超過 Persistence 基線怎麼辦？ 展現學術誠實性：如實
       報告負結果，依設計降階為「純官方歷史趨勢分析與規則防護」，不粉飾數據 14,
       39, 52-54。
  3.​ Agent 與純規則判斷有何差異？ 說明 Agent 的價值在於彈性解析使用者的多樣
       化活動情境與時間條件，但在數值運算與健康建議時，嚴格受限於確定性工具與

💡      官方規則，確保可追溯與不可篡改性 9, 15, 41, 51。
    需要為您進行下一步準備嗎？ 例如：我可以為您模擬這 10 個 Deep Research 深度問
題的口頭報告應答逐字稿，或針對後續實作期的 FastAPI 接口與資料契約（Schemas） 撰
寫細部測試規格。
```
