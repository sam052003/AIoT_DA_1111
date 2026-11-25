# AIoT_DA_1111 ↔ AirGuard-AI 文件同步紀錄

- **來源（正式系統、程式、測試與 PR）**：https://github.com/sam052003/AirGuard-AI
- **來源基準**：`main` @ `db3991181778b54dcad2867eafb54e412c450f8f`（2026-11-24 W1 與單人協作規範已合併）。
- **目標（課堂研究與提案鏡像）**：https://github.com/sam052003/AIoT_DA_1111
- **同步目的**：替換舊版 v2 的摘要、研究與 DESIGN 為 v3；新增與正式專題一致的來源、需求、實驗與 W1 文件，以及 DOCX／PPTX；重寫根 README（包含教師 Abstract A–F、Introduction、Related Work、Deep Research、Proposed Scheme）。
- **根目錄**：`README.md` 為本課堂檔案入口（為避免誤導，特別說明程式只在正式 Repo）；`DESIGN.md` 依 v3 同步並微調 W1 進度敘述；`myplan/` 同步至 v3。
- **新增資料夾**：`docs/`、`docs/proposal/`、`research/`，詳見各索引。
- **保留歷史**：`proposal/text/`、`proposal/infographics/`、`proposal/SHA256SUMS.txt` 未改寫，屬原始提案／規範的歷史文字備份。
- **保留邊界**：沒有複製 `src/`、`tests/`、`data/raw/`、`.env` 或任何 API Key；此 Repo **不是** AirGuard-AI 的第二個可執行系統。
- **即時性**：本次是**一次性快照同步，非自動同步**。未來 W2／W3 之 PR 合併後若需更新課堂 README／文件，須再次從來源最新 `main` 查核與同步。
- **測試標記**：正式 Repo W1 的離線 Python CI 與本機 API 實測應分開敘述；本次「同步文件」不構成在此 Repo 執行 ML 或 Agent 的證據。
