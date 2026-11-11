# AirGuard AI｜期末專題提案文件

> 課程：物聯網數據分析與應用（AIoT-DA）｜2026-11-03 提案版本。研究規劃不代表模型或系統已完成實驗驗證。

## 00｜原始提案文件

本目錄整理五份原始資料，原始檔需保留 DOCX／PPTX／PDF／PNG 格式以保證文字、圖片與排版完整。

| 編號 | 原始檔預定存放位置 | 說明 |
|---|---|---|
| 01 | `documents/AirGuard_AI_Final_Proposal.docx` | 正式提案報告書 |
| 02 | `slides/AirGuard_AI_Final_Proposal_Presentation.pptx` | 24 頁提案簡報 |
| 03 | `guidelines/期末專題提案作業規範.pdf` | 教師正式作業規範 |
| 04 | `analysis/AirGuard 專題提案解析.pdf` | 對照規範與 A2Z 的提案解析 |
| 05 | `infographics/AirGuard AI 專題規範落實度資訊圖表.png` | A4 橫式、十區塊編號式資訊圖表 |

**上傳狀態**：本次已先提交下方的可搜尋文字備份與索引；上述五份**二進位原始檔尚須透過 Git 推送**，不得將文字備份誤認為原件已上傳。完整原件已另行打包交付。

## 01｜GitHub 文字備份

- [正式提案報告書｜文字抽取](./text/AirGuard_AI_Final_Proposal_文字備份.md)
- [24 頁提案簡報｜文字抽取](./text/AirGuard_AI_Final_Proposal_Presentation_文字備份.md)
- [期末專題提案作業規範｜文字抽取](./text/期末專題提案作業規範_文字備份.md)
- [專題提案解析｜文字抽取](./text/AirGuard_專題提案解析_文字備份.md)
- [資訊圖表結構化重點](./infographics/INFOGRAPHIC_CONTENT.md)

文字備份可供全文搜尋，但表格、流程圖與投影片排版可能與原始檔不同。文字備份不取代原件。

## 02｜系統與研究範圍

- **Domain AI Agent × Domain Knowledge × Data Analytics × Real-World Application**。
- **三項環境部資料**：AQX_P_432（即時 AQI）、AQX_P_488（歷史 AQI）、AQX_P_13（逐時監測）。
- **預測**：1／3／6 小時 PM₂.₅，Persistence、Seasonal Naive、Ridge、Random Forest、XGBoost。
- **回測**：70／15／15 時序切分、Rolling-origin，MAE／RMSE／Skill Score。
- **Agent**：受控工具呼叫、官方 AQI 規則、來源追溯、至少 30 項情境驗收與安全降級。
- **限制**：PM₂.₅ 預測不是未來官方 AQI，測站資料非街道級個人暴露；無個人醫療診斷。

## 03｜完整性與後續工作

- 原始檔 SHA-256 檢查碼見 [SHA256SUMS.txt](./SHA256SUMS.txt)。
- 研究／開發計畫請見 [myplan/](../myplan/)。
- 提案階段的 Expected Outcomes 不是完成的實驗結果。
- 後續仍需建立並維護根目錄 `DESIGN.md`、可重現實驗與 Demo，才能符合完整 Final Handover 規範。
