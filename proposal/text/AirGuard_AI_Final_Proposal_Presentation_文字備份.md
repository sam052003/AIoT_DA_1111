# AirGuard_AI_Final_Proposal_Presentation.pptx｜文字備份

> 此檔為原始「AirGuard_AI_Final_Proposal_Presentation.pptx」的**自動抽取文字備份**，僅供 GitHub 搜尋與檢閱。圖表、版面、圖片與表格格式可能未完整保留；原始檔仍應以 DOCX／PPTX／PDF 為準。提案階段，非實作驗證成果。

---

```text


























AirGuard AI｜Final Project Proposal Presentation





AIRGUARD  AI
智慧空氣品質預測與生活決策代理人
DOMAIN AI AGENT  ×  OPEN DATA  ×  DATA ANALYTICS

Final Project Proposal  /  物聯網數據分析與應用
2026.11.03  |  Research & Design Stage  | 林宏陽 / 7115056179 （組長） 、蔡明憲 / 7115056013、許鈵昆 / 8114056002
空氣品質預測 × 領域知識 × 可解釋決策支援



1


01 · MOTIVATION
研究核心：從空污資訊走向行動決策
從資訊展示轉為「空污預測 × 風險解釋 × 行動決策」

AirGuard AI  •  AIoT-DA  •  Proposal / 2026.11.03
02

DATA
環境部官方即時 / 歷史空污資料

ANALYTICS
PM2.5 1 / 3 / 6 小時短期預測

DOMAIN KNOWLEDGE
AQI 指引與敏感族群活動規則

AI AGENT
理解需求、調工具、整合證據




研究問題
如何將監測站污染資料與可信預測，轉換成有證據、可追溯、可安全降級的戶外活動建議？
設計原則：官方 AQI ≠ 模型 PM2.5 預測；Agent 不得把預測說成官方數據。



2


01 · MOTIVATION
Why now?｜有公衛意義，也有現成資料
用 2025–2026 公開證據說明問題價值

AirGuard AI  •  AIoT-DA  •  Proposal / 2026.11.03
03

420 萬人
WHO 估計 2019 年室外空污造成的過早死亡人數

12.8 μg/m³
臺灣 2025 年 PM2.5 手動測站年平均濃度

長期空品改善 ≠ 個別時段的活動風險自動消失
Sources: WHO (2024); Taiwan MOENV Air Quality Management (2026, reporting 2025 statistics).



3


01 · RESEARCH OBJECTIVES
研究目標與可驗證成果
明確定義研究問題、系統能力與評估方式

AirGuard AI  •  AIoT-DA  •  Proposal / 2026.11.03
04

項目

研究目標 / 系統能力

預期驗證方式

研究問題

將空污數據轉為活動建議

情境案例與決策依據

Agent 能力

規劃任務、調用工具

工具選擇與來源完整率

污染預測

1 / 3 / 6h PM2.5 預測

MAE / RMSE、基線比較

風險指引

依官方 AQI 規則解釋風險

建議規則一致性測試

系統可靠性

缺值、過期與錯誤降級

安全降級率、P95 延遲
研究核心：Data Acquisition → Forecasting → Domain Validation → Evidence-grounded Decision。



4


02 · ABSTRACT
Abstract Story：A → F
六段式研究故事與老師規範對齊

AirGuard AI  •  AIoT-DA  •  Proposal / 2026.11.03
05


A
Attention Getter
空污仍有公衛影響


B
But / Gap
資訊到決策的落差


C
Cure
提出 AirGuard AI


D
Development
API + ML + Agent + Rules


E
Experiments
時序回測 + 情境測試


F
Expected Findings
可驗證原型與侷限
Proposal 的 Findings 一律寫 Expected Outcomes，不預設已完成實驗。



5


02 · INTRODUCTION
Application Scenario｜活動前做決策
情境輸入將觸發資料查詢、預測與領域規則查核

AirGuard AI  •  AIoT-DA  •  Proposal / 2026.11.03
06

USER QUERY
「明天早上 7 點
我想在臺中慢跑 40 分鐘，
哪個時段比較適合？」

01
確認地點、時段與族群

02
查官方 AQI + 最新污染數值

03
預測 PM2.5 趨勢與不確定性

04
檢查官方活動指引及限制

05
提供候選時段與資料來源
不會提供個人醫療診斷；測站尺度資料也不代表街道級暴露。



6


03 · LITERATURE
Related Work｜AI Technology
預測模型 × 可解釋分析 × 工具導向 Agent

AirGuard AI  •  AIoT-DA  •  Proposal / 2026.11.03
07


2026
Chianese & Riccio
空品預測綜述
模型選擇需看時距、驗證方式


2025
Joseph & Ganapathy
PM2.5 時序方法回顧
比較統計、ML、DL 方法


2024
Houdou et al.
Interpretable ML Review
SHAP 有助理解，非因果證據


2023
Yao et al. / ReAct
Reasoning + Acting
支援 Agent 調工具架構


2025
Nie & Liu
LLM Environmental Decisions
輔助式角色優於過度自主
Sources: doi:10.3390/forecast8040072; 10.1016/j.fraope.2025.100372; 10.4209/aaqr.230151; ReAct (ICLR 2023); 10.1016/j.jenvman.2025.124373.



7


03 · LITERATURE
Related Work｜Domain Know-how
實體污染物、台灣 AQI 規則、官方資料治理

AirGuard AI  •  AIoT-DA  •  Proposal / 2026.11.03
08


2021 / 2024
WHO
健康暴露指引、全球健康負擔


2025 起
MOENV
臺灣 AQI 門檻／活動指引／多污染物副指標


2026
MOENV
AQX_P_432 / 488 / 13；官方資料與時戳


2025
Lo et al.
臺灣地面監測＋衛星／土地利用的 XGBoost、SHAP


2025
Gao et al.
大型語言模型處理野火 GIS／空品資訊案例
Sources: WHO AQG (2021), WHO (2024), MOENV AQI official guidance and datasets, Lo et al. (2025), Gao et al. (2025).



8


03 · LITERATURE
Article Summary Table｜精選文獻對照
完整 8 欄版本已放入 Proposal Document；此頁選取 6 篇

AirGuard AI  •  AIoT-DA  •  Proposal / 2026.11.03
09

Ref

Year

Problem

AI Method

Domain

Dataset

Findings

Limitation

[3]

2026

評估跨情境

Mapping Review

污染物／時距

409 papers

無通用最佳

需情境驗證

[11]

2024

可解釋性

SHAP Review

空污因素

Review

可理解性

非因果

[12]

2023

Agent 使用工具

ReAct

可靠資訊

QA/tasks

工具推理

非空污專用

[8]

2025

環境決策

LLM Framework

環境模型

Case study

輔助決策

監督需求

[15]

2025

臺灣 PM2.5

XGB + SHAP

地理／衛星

28 stations

時空估計

非即時建議

[14]

2025

臺灣 AQI

Official Rules

活動指引

MOENV

正式分級

非醫療診斷
原始來源與 DOI／URL 已列於報告書 References；本頁只摘要最關鍵的文獻特徵。



9


03 · RESEARCH GAP
Research Gap：我們要驗證的缺口
不是聲稱世界上沒有相似系統，而是提出可測的整合式假設

AirGuard AI  •  AIoT-DA  •  Proposal / 2026.11.03
10

01
Existing Research
官方 AQI 監測／預報
PM2.5 模型與 XAI
工具使用 LLM


02
Limitations
單獨模型不等於行動建議
數據時效與規則可能脫節
評估缺乏端到端情境


03
Research Gap
缺少同時測試預測、
證據追溯、規則一致性、
錯誤降級的臺灣原型比較


04
AirGuard AI
資料 → 預測 → 規則 → 決策
可追溯 Agent 系統
雙軌客觀評估
Gap 的新穎性須持續文獻檢索；Proposal 的目標是提出可檢驗的差異化設計。



10


04 · DEEP RESEARCH
Deep Research Q1｜5 個核心思維模式
專業知識不是只放進 RAG；應反映到系統設計

AirGuard AI  •  AIoT-DA  •  Proposal / 2026.11.03
11


01
暴露與活動導向
把位置、時段、活動、族群視為決策變數


02
時空／單位一致性
站點、時間戳、平均窗、單位須可驗證


03
Baseline 與防洩漏
先用 Persistence + rolling-origin 檢驗模型


04
可解釋但不過度宣稱
特徵重要性不是污染因果關係


05
人本與安全降級
資料不足時承認未知、回到官方資訊
Evidence: WHO (2021, 2024), MOENV AQI (2025), Chianese & Riccio (2026), Houdou et al. (2024), Nie & Liu (2025).



11


04 · DEEP RESEARCH
Deep Research Q2｜3 個關鍵爭論
A ↔ B → Evidence → Consensus → Unresolved Problems

AirGuard AI  •  AIoT-DA  •  Proposal / 2026.11.03
12

01 模型複雜度

Deep Learning / GNN
↕

Persistence / Tree Models
Consensus  沒有普遍最佳模型；要看場景與回測。
Unresolved  特定站點 1–6h 是否值得加大模型？

02 預測 vs 可解釋

追求最低 RMSE
↕

來源、限制與可解釋
Consensus  效能與可用性都需要驗證。
Unresolved  使用者願如何權衡兩者？

03 Agent 自主程度

完全自主 Agent
↕

規則約束＋監督
Consensus  環境決策中的 LLM 宜保留護欄。
Unresolved  什麼條件下應拒答或降級？
Sources: Chianese & Riccio (2026); Houdou et al. (2024); Nie & Liu (2025).



12


04 · DEEP RESEARCH
Deep Research Q3｜10 個理解深度問題
從記憶事實進一步測試系統設計的思辨能力

AirGuard AI  •  AIoT-DA  •  Proposal / 2026.11.03
13

01
Why：PM2.5 目前值為何不等於官方 AQI？

02
What-if：API 過期兩小時，Agent 怎麼做？

03
Trade-off：複雜模型僅微幅改善 MAE 值得嗎？

04
Failure：隨機切分為何可能洩漏未來資訊？

05
Evidence：如何驗證活動建議符合官方規則？

06
Comparison：1h 與 6h 預測為何不能只看平均？

07
Design：為何將 Agent、ML、Domain Rules 分離？

08
Scenario：隔壁測站正常，能推薦該街區嗎？

09
Uncertainty：區間跨風險門檻時如何回覆？

10
Causality：SHAP 的重要風速代表因果嗎？
深度問題涵蓋推理、設計取捨、證據判讀與失效情境。



13


05 · PROPOSED SCHEME
Proposed Design｜MVP 與延伸範圍
先保證可做完的可驗證核心，避免功能過度膨脹

AirGuard AI  •  AIoT-DA  •  Proposal / 2026.11.03
14

MVP / 必做

環境部即時 AQI + 歷史污染物資料管線

PM2.5 1 / 3 / 6 小時預測 + Baseline 比較

可用 Tool Calling 的 Agent 與資料查核

官方 AQI 活動建議規則引擎

情境化決策頁面 + 評估 Dashboard

Stretch / 選做

24 小時趨勢預測

多測站時段比較

地點選擇與路徑替代

異常污染事件警示

回饋蒐集與使用者測試
MVP 所有輸出保留資料時間、站點、證據來源及不確定性。



14


05 · ARCHITECTURE
System Architecture｜8 個編號模組
與報告書的 ①–⑧ 逐一對應

AirGuard AI  •  AIoT-DA  •  Proposal / 2026.11.03
15

①
User / Web UI
情境輸入


②
Query Interpreter
意圖、時間、地點


③
Planner Agent
工具與任務規劃


④
Data Acquisition
即時 API／歷史 CSV

⑤
Analytics Engine
ML 預測／XAI


⑥
Domain Rules
官方 AQI 活動規範


⑦
Decision Engine
時段與風險比較


⑧
Output & Logs
可追溯互動輸出


Common Controls   freshness  •  provenance  •  uncertainty  •  audit trail  •  human oversight



15


05 · FLOWCHART
Flowchart｜帶有決策與例外處理
資料不足不強行給建議

AirGuard AI  •  AIoT-DA  •  Proposal / 2026.11.03
16

INPUT
活動條件 + 站點


PLANNER
Agent 選工具


RETRIEVAL
官方 AQI + 歷史


QUALITY CHECK
新鮮度／完整性？

ANALYTICS
PM2.5 + 不確定性


DOMAIN RULES
官方活動指引


DECISION
時段比較、保守建議


OUTPUT
來源／限制／時間戳


QUALITY CHECK = NO   →   不推測即時狀態，顯示資料不足、官方來源與安全降級



16


06 · DATA ANALYTICS
Data Plan｜官方來源與資料契約
Training data 與 Online data 分開，來源與單位透明

AirGuard AI  •  AIoT-DA  •  Proposal / 2026.11.03
17


AQX_P_432
即時 AQI
siteid · aqi · pm2.5 · publishtime
每小時更新（官方 metadata）


AQX_P_488
歷史 AQI
siteid · pm2.5 · windspeed · time
歷史月檔可下載


AQX_P_13
小時觀測
monitorvalue00…23 → long format
每小時觀測、每日更新


MOENV AQI Guide
領域知識
AQI 分級 · 一般／敏感族群
2025 起使用修訂門檻
Target：PM2.5 原始每小時濃度（μg/m³）；官方即時 AQI 仍以環境部發布值為準。



17


06 · MODELING
Analytics Pipeline｜先嚴格回測再上線
模型越複雜並非一定越準；須優於簡單基線

AirGuard AI  •  AIoT-DA  •  Proposal / 2026.11.03
18

01
資料清理
timestamp、units、missing values

02
特徵工程
lags 1/3/6/12/24h、rolling

03
時序切分
70/15/15 chronological + rolling

04
模型對比
Persistence、Ridge、RF、XGB

05
回測分析
MAE、RMSE、分站、分時距

06
模型版本化
推論、誤差區間、SHAP
防洩漏：所有預測時刻 t 只能使用當時已可得的特徵；test set 不用來調參。



18


06 · ALGORITHM
Pseudocode｜Core Agent Algorithm
核心程序：工具調度、模型預測、領域規則與證據查核

AirGuard AI  •  AIoT-DA  •  Proposal / 2026.11.03
19

01  request = parse_intent(query)
02  plan = select_allowed_tools(request)
03  live = retrieve_official_aqi(station)
04  hist = retrieve_recent_pm25(station)
05  quality = validate(site,time,unit)
06  if not quality.ok: safe_fallback()
07  latest_aqi = live.official_aqi
08  X = make_past_only_features(hist)
09  pred = forecast(X, h=[1,3,6])
10  bands = estimate_uncertainty(pred)

11  rules = load_official_aqi_rules()
12  candidates = compare_time_windows()
13  decision = conservative_rank()
14  evidence = [live,pred,bands,rules]
15  result = compose_with_sources()
16  result = validate_claims(result)
17  assert official_aqi != predicted_pm25
18  if invalid: return safe_fallback()
19  save_audit_trace()
20  return explainable_recommendation
流程重點：官方資料由工具提供；數值預測由 ML 提供；健康指引由規則服務提供。



19


07 · EXPERIMENTS
Evaluation Plan｜雙軌驗證
模型預測與 Agent 決策採雙軌評估

AirGuard AI  •  AIoT-DA  •  Proposal / 2026.11.03
20

TRACK A  /  ML FORECASTING

Horizon：1 / 3 / 6 hours

Baseline：Persistence、Seasonal Naive

Models：Ridge、Random Forest、XGBoost

Metrics：MAE、RMSE、Skill vs Baseline

Protocol：Time split + Rolling-origin

Breakdown：站點／季節／污染高峰

TRACK B  /  AGENT & DECISION

至少 30 個 Agent 測試情境

工具選擇正確率 / 來源完整率

官方規則一致性

缺值、過期、API 錯誤的降級行為

Median / P95 回應時間

人工檢視保守性與限制陳述
假設：2024–2026 期間可用歷史資料；實際範圍待資料品質盤點後確認。



20


07 · TECHNICAL FEASIBILITY
Risk Management｜明確設定 Fail-safe
風險不是附註，而是設計的一部分

AirGuard AI  •  AIoT-DA  •  Proposal / 2026.11.03
21

資料延遲 / API 錯誤
→
快取、時戳顯示、拒絕假即時輸出

預測不優於 Baseline
→
誠實報告；降階為趨勢與規則分析

模型產生誤導解釋
→
標示不確定性；SHAP 非因果

健康建議過度自信
→
官方 AQI 規則優先；不做醫療診斷

站點空間代表性不足
→
明示「測站尺度」，不推論街道級暴露

核心政策：Source-grounded / Timestamped / Uncertainty-aware / No hallucinated health advice



21


08 · HANDOVER
Roadmap & Deliverables
六個階段由資料到 Final Handover

AirGuard AI  •  AIoT-DA  •  Proposal / 2026.11.03
22

W1
資料盤點
EDA & schema


W2
預測基線
Backtest


W3
Agent & Rules
Tool tests


W4
Web Prototype
Live demo


W5
實驗與消融
Evaluation


W6
Final Package
Docs / Video

FINAL HANDOVER｜可重現交付
Source Code   ·   Data Sources   ·   README   ·   DESIGN   ·   Experiments   ·   Demo
交付內容包含部署、測試、資料處理與模型重現步驟。



22


08 · CONCLUSION
Expected Contributions & Limitations
評估完成後以實際數據驗證預期貢獻

AirGuard AI  •  AIoT-DA  •  Proposal / 2026.11.03
23

EXPECTED OUTCOMES

可執行的 Domain AI Agent 網頁原型

可重現的 PM2.5 Baseline / ML 比較

官方規則 + 可追溯解釋

Agent 情境測試與安全降級

完整 README / DESIGN 與 Demo

KNOWN LIMITATIONS

測站不能代表每一條街道

PM2.5 預測不是完整 AQI 預報

不保證模型超越 Baseline

不提供醫療診斷／健康結果保證

歷史資料品質／API 限制仍待驗證
以既定實驗流程檢驗模型、Agent 與決策規則的可靠性。



23


09 · REFERENCES
Key References & Data Sources
資料來源均為官方網站或已公開的同行評審／學術文獻

AirGuard AI  •  AIoT-DA  •  Proposal / 2026.11.03
24

[1] WHO (2024). Ambient (outdoor) air pollution. who.int

[2] Taiwan MOENV (2026). Air Quality Management / 2025 statistics. moenv.gov.tw


[3] Chianese & Riccio (2026). Forecasting 8(4), 72. doi:10.3390/forecast8040072

[4] Nie & Liu (2025). Journal of Environmental Management. doi:10.1016/j.jenvman.2025.124373

[5] Gao et al. (2025). Int. J. Applied Earth Observation. doi:10.1016/j.jag.2025.104774

[6] Lo et al. (2025). Science of the Total Environment. doi:10.1016/j.scitotenv.2025.180050

[7] Houdou et al. (2024). Aerosol and Air Quality Research. doi:10.4209/aaqr.230151

[8] Yao et al. (2023). ReAct, ICLR. arxiv.org/abs/2210.03629

[9] MOENV Data: AQX_P_432, AQX_P_488, AQX_P_13. data.moenv.gov.tw

[10] MOENV. AQI Health & Activity Guidance. airtw.moenv.gov.tw

完整文獻資訊與資料來源詳見提案報告書 References。



24

```
