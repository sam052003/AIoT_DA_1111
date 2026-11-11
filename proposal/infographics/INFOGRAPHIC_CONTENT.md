# AirGuard AI｜專題規範落實度資訊圖表（文字導覽）

> 原件：`AirGuard AI 專題規範落實度資訊圖表.png`。本文件是便於 GitHub 搜尋的**人工結構化摘要**，不是圖片或圖片內文字的逐字稿。圖表評估的是「規劃文件涵蓋內容」，並非已完成實作驗收。

## 01｜總體規範符合度
Domain AI Agent、Domain Knowledge、Data Analytics、Real-World Application 四支柱；官方即時 AQI、短時 PM₂.₅ 預測、活動指引與受約束 Agent 分工。

## 02｜Abstract A–F
Attention（全球／臺灣空污問題）、But（展示與決策斷層）、Cure（AirGuard AI）、Development（官方資料、ML、Agent）、Experiments（ML 回測／Agent 測試）、Findings（Expected Outcomes）。

## 03｜Related Work
AI 技術 × Domain Know-how；Article Summary Table；Existing Research → Limitations → Research Gap → Our Project。

## 04｜Deep Research
五個核心思維模式、三項專業爭論與十題深入理解問題；重視時空一致、基線、防洩漏、可解釋與安全降級。

## 05｜Proposed Scheme
八模組：① User/Web UI → ② Query Interpreter → ③ Planner Agent → ④ Data Acquisition → ⑤ Analytics Engine → ⑥ Domain Rules → ⑦ Decision Engine → ⑧ Output & Interaction。
包含 Quality Check 的例外分支，以及 AirGuardAgent／TrainAndEvaluate 雙演算法偽程式碼。

## 06｜Experiments & Evaluation
Track A：1／3／6h PM₂.₅；Persistence／Seasonal Naive 與 Ridge／RF／XGBoost；MAE、RMSE、Skill Score、Rolling-origin。
Track B：至少 30 個 Agent 情境；工具選擇、來源完整、規則一致及降級能力。

## 07｜Roadmap & Risks
W1 資料盤點 → W2 基線回測 → W3 Agent → W4 Web → W5 雙軌評估 → W6 成果交接；風險含資料延遲、模型未勝基線、LLM 幻覺、測站尺度限制。

## 08｜A2Z outline 對照
Abstract（A–F）、Introduction、Related Work、Proposed Scheme、Simulation／Evaluation、Conclusion；以章節設計映射提案結構。

## 09｜規範落實度七大維度
摘要／緒論、文獻研究、Deep Research、系統設計、評估設計、專案規劃、整體一致性。圖表的「符合」係指**提案文件已描述**相關規劃。

## 10｜Conclusion
提案 DOCX 與 PPTX 提供相互補充的研究主張；實際模型效能、決策品質及終端使用者效益均須於實作期驗證。

詳見 [正式提案文字備份](../text/AirGuard_AI_Final_Proposal_文字備份.md)、[簡報文字備份](../text/AirGuard_AI_Final_Proposal_Presentation_文字備份.md)。
