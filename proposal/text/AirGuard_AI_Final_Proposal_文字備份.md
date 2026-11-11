# AirGuard_AI_Final_Proposal.docx｜文字備份

> 此檔為原始「AirGuard_AI_Final_Proposal.docx」的**自動抽取文字備份**，僅供 GitHub 搜尋與檢閱。圖表、版面、圖片與表格格式可能未完整保留；原始檔仍應以 DOCX／PPTX／PDF 為準。提案階段，非實作驗證成果。

---

```text
<PARSED TEXT FOR PAGE: 1 / 22>

                                        AIRGUARD AI / FINAL PROJECT PROPOSAL




             AirGuard AI
       智慧空氣品質預測與生活決策代理人

       Final Project Proposal · 期末專題提案報告書




專題資訊    內容

專題名稱    AirGuard AI｜智慧空氣品質預測與生活決策代理人

課程名稱    物聯網數據分析與應用（AIoT-DA）

        林宏陽 / 7115056179 （組長）

組員姓名    蔡明憲 / 7115056013

        許鈵昆 / 8114056002

        Domain AI Agent × Open Data × PM2.5 Forecasting ×
研究定位
        Explainable Decision Support

文件資訊    Final Project Proposal｜2026 年 11 月 3 日

                                       AIoT-DA · 2026.11.03 · Final Project Proposal

<PARSED TEXT FOR PAGE: 2 / 22>

                         AIRGUARD AI / FINAL PROJECT PROPOSAL




研究主張：從「查詢當前 AQI」走向「結合可信資料、短期預測與官方健康指引的可追溯活

                 動決策支援」。




                        AIoT-DA · 2026.11.03 · Final Project Proposal

<PARSED TEXT FOR PAGE: 3 / 22>

                                       AIRGUARD AI / FINAL PROJECT PROPOSAL


摘要 Abstract｜A–F Research Story

A. Attention Getter — Motivation

空氣污染影響民眾的戶外活動決策。WHO 估計 2019 年室外空污造成約 420 萬人過早死

亡；環境部資料顯示臺灣 2025 年手動測站 PM2.5 年平均濃度為 12.8 μg/m³。儘管長期空

品改善，時段、地點與敏感族群的暴露風險仍需要具時效性的判斷 [1][2]。


B. But — Challenge

既有服務能顯示即時監測指標或區域預報，但使用者仍需自行將污染變化、活動時間、健康

風險及資料有效性轉譯為行動。ML 預測研究則常面臨時序資料洩漏、解釋不足與缺乏行動

情境驗證等挑戰 [3][4]。


C. Cure — Proposed Solution

本專題提出「AirGuard AI：智慧空氣品質預測與生活決策代理人」，以「問題理解→資料

檢索→PM2.5 短期預測→領域規則查核→可解釋建議」協助使用者評估戶外活動時段。


D. Development — Method

擬整合環境部 AQX_P_432 即時 AQI、AQX_P_488 歷史 AQI 與 AQX_P_13 監測小時值；使

用 Persistence、Ridge/Random Forest、XGBoost 等模型比較 1/3/6 小時 PM2.5 預測；

由工具導向 Agent 呼叫資料與模型服務，並由官方 AQI 建議規則約束輸出 [5]–[7]。


E. Experiments — Evaluation

預計採時間先後切分與 rolling-origin 回測，報告 MAE、RMSE、不同預測時距及測站的誤

差；以情境測試評估 Agent 工具選擇、證據溯源、官方規則一致性、缺值時安全降級與延

遲。




                                      AIoT-DA · 2026.11.03 · Final Project Proposal

<PARSED TEXT FOR PAGE: 4 / 22>

                                            AIRGUARD AI / FINAL PROJECT PROPOSAL

F. Findings — Expected Outcomes

本研究預期完成可操作的網頁系統、可重現的模型基線比較、具明確來源的活動建議與系統

設計文件。預測精度、模型相對增益與使用者效益將依後續實驗結果報告。


關鍵字 Keywords

Domain AI Agent；Air Quality；PM2.5 Forecasting；Explainable AI；Open Data；

Decision Support



1. Introduction｜緒論

1.1 Attention Getter｜問題的重要性

WHO 指出，2019 年約有 99% 世界人口居住於未符合其空氣品質指引的地區，室外空污造

成約 420 萬人過早死亡 [1]。環境部 2026 年發布的 2025 年空品統計指出，臺灣 PM2.5 手

動站年平均為 12.8 μg/m³，長期趨勢雖改善，但區域及短時污染變動仍是戶外活動的重要

資訊 [2]。


1.2 Background｜領域、使用者與資料背景

使用者包括一般戶外運動者、通勤者與需留意空污之敏感族群。臺灣環境部提供測站層級的

每小時 AQI、污染物數值、地理資訊與歷史資料，可不依賴自建感測器進行原型驗證 [5]–

[7]。本系統以「測站尺度」為最小可驗證空間單位，不宣稱精確到每條街道。


1.3 Problem Definition｜問題定義

輸入為使用者的活動類型、城市／監測站、規劃時段與一般／敏感族群選項；輸出應包含官

方最新 AQI、1–6 小時 PM2.5 趨勢預測、活動風險說明、候選時段比較、資料來源及不確定

性。核心任務並非單純回答「目前 AQI 是多少」，而是在資訊不足時仍能做出安全而可追

溯的決策支援。


                                           AIoT-DA · 2026.11.03 · Final Project Proposal

<PARSED TEXT FOR PAGE: 5 / 22>

                                  AIRGUARD AI / FINAL PROJECT PROPOSAL


1.4 Existing Limitations｜現有方法限制

   資料展示與實際行動存在落差：使用者需要自行解讀 AQI、污染物、活動強度與時段。

   模型比較容易忽略部署條件：不同預測時距、訓練／測試切分與資料洩漏會改變效能 [3]

    [4]。

   生成式語言模型若未被工具及規則約束，可能誤引過期數據、混淆官方 AQI 與 PM2.5 預

    測或提供過度確定的健康判斷 [8][9]。


1.5 Innovation｜擬議差異化設計

   情境式 Agent：不是聊天框附加在儀表板，而是可規劃查詢、預測、規則檢核與回覆的

    工作流。

   雙軌證據：即時 AQI 只使用官方指標；模型另預測 PM2.5 濃度及其不確定性，不將單一

    污染物直接當成官方 AQI。

   可驗證決策：同時量測預測誤差、建議規則一致性、來源完整率及 API 失效時的安全降

    級。

   情境式決策閉環：結合使用者活動條件、污染趨勢與官方指引，輸出候選時段、風險解

    釋、可信度及可追溯證據。


1.6 Expected Contributions｜預期貢獻

1. 提供基於官方開放資料的 PM2.5 短期預測可重現比較流程。

2. 提出 Agent–Analytics–Domain Rule 三層分離、具證據追溯的系統架構。

3. 建立資料新鮮度、缺漏、風險與活動建議一致性的測試集合。

4. 完成可供非原開發者維護的系統文件與可操作 Demo。




                                 AIoT-DA · 2026.11.03 · Final Project Proposal

<PARSED TEXT FOR PAGE: 6 / 22>

                                      AIRGUARD AI / FINAL PROJECT PROPOSAL


2. Related Work｜相關研究

2.1 AI Technology｜預測模型與 AI Agent

2026 年 Chianese 與 Riccio 的研究整理 409 篇符合條件的空品預測文獻，指出模型優劣依

污染物、預測時距、感測網密度與評估方式而異，沒有適用所有情境的單一模型 [3]。2025

年 Joseph 與 Ganapathy 的 PM2.5 時間序列回顧則整理統計、ML 與深度學習方法的比較

面向 [10]。本計畫因此以容易部署的樹模型搭配簡單基線，優先證明預測增益與回測有效性，

而非預設深度網路一定更準。

Houdou 等人的系統性回顧指出，SHAP 等可解釋機制有助於讓空污預測對非專家更可理解，

但解釋不代表因果證據 [11]。ReAct 提供語言模型交替進行推理與工具操作的設計參考

[12]；Nie 與 Liu 的環境決策研究則提醒，LLM 更適合在可監督的助理角色下運作 [8]。


2.2 Domain Knowledge｜空污與健康活動指引

WHO 空氣品質指引提供長短期污染暴露的健康風險依據，並非供系統直接診斷個人疾病的

標準 [1][13]。臺灣環境部自 2025-01-01 調整 AQI 濃度門檻，官方 AQI 涵蓋 O3、PM2.5、

PM10、CO、SO2、NO2 等污染物副指標，且使用不同時間平均方式；因此「單看 PM2.5

的即時量測或預測值」不能直接等同完整 AQI [14]。

Lo 等人 2025 年在臺灣以地面測站、衛星資訊與土地利用模型結合 XGBoost、SHAP 估計

PM2.5 成分的時空變異，顯示本地領域知識與地理差異的重要性 [15]。環境部現有資料提

供測站位置、每小時污染數值及風場等欄位，適合建立以測站為單位、明確標示來源與時間

戳的決策支援原型 [5]–[7]。


2.3 Literature Selection & Evidence Quality

文獻選擇涵蓋空污預測、可解釋機器學習、工具導向 AI Agent，以及 WHO 與環境部的領域

指引。Article Summary Table 同時納入實證研究、方法文獻與官方規範，並分別標示資料

型態、主要發現及研究限制。
                                     AIoT-DA · 2026.11.03 · Final Project Proposal

<PARSED TEXT FOR PAGE: 7 / 22>

                                     AIRGUARD AI / FINAL PROJECT PROPOSAL


2.4 Existing Research → Limitations → Research Gap → Our

Project

 階段             歸納

 Existing       (a) 公開監測資料與官方 AQI 指引；(b) PM2.5 預測方法；(c) XAI

 Research       與具工具能力 LLM。

                預測研究未必提供面向一般使用者的決策流程；純聊天型介面可能
 Limitations
                有資料新鮮度、可追溯性與官方規則不一致的風險。

                在臺灣測站尺度，短期預測、官方活動指引、資料時效與 AI Agent
 Research Gap
                工具行為的整合式驗證，仍有值得研究的系統性比較空間。

                以可重現回測 + 官方 AQI 規則 + 降級機制 + 情境式 Agent 實作並
 Our Project
                測試此設計主張。



本研究聚焦的缺口為：在臺灣測站尺度，如何以統一評估設計整合短期 PM2.5 預測、官方

活動指引與具證據追溯能力的 AI Agent，並驗證其在資料不完整情境下的決策可靠性。




                                    AIoT-DA · 2026.11.03 · Final Project Proposal

<PARSED TEXT FOR PAGE: 8 / 22>

                                                                                  AIRGUARD AI / FINAL PROJECT PROPOSAL


2.5 Article Summary Table｜AI Technology × Domain Know-how

       Yea                                     Domain
Ref.         Problem        AI Method                       Dataset   Findings                      Limitation
       r                                       Knowledge


       202   跨情境空污預測研 Systematic               污染物、時距、                無通用最佳模型；驗證設                   屬綜述；非臺灣部署
[3]                                                         409 篇文獻
       6     究比較            Mapping            驗證設計                   計重要                           實驗


       202   PM2.5 預測方法盤 Statistical/ML/                                                            沒有直接驗證本系統
[10]                                           PM2.5 時序特性   研究論文      比較不同預測方法與指標
       5     點              DL Review                                                               Agent


       202                  Interpretable ML                          可解釋機制支持非專家溝                   解釋非因果、未保證
[11]         預測可解釋性不足                          污染變數解釋       系統性回顧文獻
       4                    / SHAP                                    通                             決策改善


       202   LLM 如何與工具                                                交替推理與工具操作可提                   非空污專用；需加領
[12]                        ReAct              需外部可靠資訊      QA/互動任務
       3     協作                                                       升任務表現                         域規則


       202   LLM 環境決策框      LLM-assisted/                             LLM 有助決策工作流；助 自主性與可靠性仍有
[8]                                            環境決策需監督      環境模型情境
       5     架              driven                                    理更合適                          限

       202   野火空品分析與建 Instructor–              野火／GIS／空品 2025 洛杉磯野火   展示 Agent 串接雲端環                案例專屬；非臺灣常
[9]
       5     議              Worker LLM         情境           案例        境資訊                           態活動情境



                                                                                 AIoT-DA · 2026.11.03 · Final Project Proposal

<PARSED TEXT FOR PAGE: 9 / 22>

                                                                                  AIRGUARD AI / FINAL PROJECT PROPOSAL


       Yea                                   Domain
Ref.         Problem       AI Method                     Dataset      Findings                      Limitation
       r                                     Knowledge

                                                                                                    估計月尺度離子成
       202   臺灣 PM2.5 成分   LUR + XGBoost +   衛星、土地利      臺灣 28 站 /
[15]                                                                  說明在地空污變數有影響                   分；非每小時活動建
       5     空間變異          SHAP              用、地面觀測      2019–2021
                                                                                                    議


       202                                   濃度／平均時間                                                全球健康指引非臺灣
[13]         空污健康暴露準則 循證指引                               WHO 證據整合     建立污染暴露判斷背景
       1                                     ／健康風險                                                  AQI 規則


       202   臺灣 AQI 分級與                      副指標、敏感族                  可作可驗證的安全規則來                   無個人精細暴露與個
[14]                       官方規則                          環境部標準
       5     活動指引                            群                        源                             別醫療判斷

[5]–   202   資料取得與可追溯                        測站、時戳、污     MOENV 歷史／即                                 資料缺失、延遲、站
                           Open Data/API                              支援免感測器原型與回測
[7]    6     性                               染物          時                                          點代表性



表 1. 相關研究、技術方法與領域知識對照；來源包括學術研究、官方規範及資料集。




                                                                                 AIoT-DA · 2026.11.03 · Final Project Proposal

<PARSED TEXT FOR PAGE: 10 / 22>

                                     AIRGUARD AI / FINAL PROJECT PROPOSAL



3. Deep Research｜三大核心問題

Q1. 五個核心思維模式（Mindsets）

1. Exposure over visualization（暴露與行為導向）

意義：重點不是圖表多漂亮，而是使用者在何時、何地活動，以及污染對不同族群的影響。

證據：WHO 健康暴露指引與 MOENV 活動建議 [13][14]。

系統影響：Query schema 必須包含時段、地點、活動與族群；結果避免醫療診斷。


2. Spatiotemporal fidelity（時空一致性）

意義：站點／時間戳／平均時間若混淆，容易產生誤導。

證據：MOENV 資料欄位與即時 AQI 計算方法 [5]–[7][14]。

系統影響：所有觀測值附測站 ID、time zone、更新時間、單位；不可混用不同平均窗。


3. Baseline-first and leakage-safe（先驗證再複雜化）

意義：使用 Persistence 及按時間切分，不能靠隨機切分得到過度樂觀結果。

證據：2026 年系統性綜述及 leakage-aware 研究 [3][4]。

系統影響：先做 persistence、rolling-origin，固定同一資料切分比較模型。


4. Explain without overclaim（可解釋但不過度因果化）

意義：重要特徵有助理解，但 SHAP 不等於已證實污染來源或因果機制。

證據：可解釋空污 ML 回顧 [11]。

系統影響：顯示模型特徵重要性、預測誤差、限制，不做因果結論。


5. Human-centered, fail-safe agent（人本與安全降級）

意義：Agent 應主動查證與承認未知；資料錯誤時寧可拒絕精確判斷。


                                    AIoT-DA · 2026.11.03 · Final Project Proposal

<PARSED TEXT FOR PAGE: 11 / 22>

                                  AIRGUARD AI / FINAL PROJECT PROPOSAL

證據：環境決策 LLM 研究及 ReAct [8][12]。

系統影響：資料新鮮度守門、工具白名單、官方規則優先、留存輸出與依據。


Q2. 三個最重要的專業爭論（Controversies）

爭論 1：模型越複雜越好？

A｜Transformer / GNN 可表達複雜時空關係；在資料量大、空間關聯強的條件下可能有

效。

B｜Persistence、樹模型較易重現、解釋、部署，少量資料亦常有競爭力。

Evidence / Consensus：2026 年綜述指出無普遍最佳模型，應依預測時距、資料供應與驗

證框架選取 [3]。

Unresolved Problems：臺灣特定測站／1–6 小時預測是否值得使用深度模型，需在相同切

分實測。


爭論 2：準確預測 vs 可解釋與安全

A｜以 MAE/RMSE 為核心，優先最大化數值預測品質。

B｜強調特徵解釋、資料新鮮度、風險表述與規則一致性。

Evidence / Consensus：XAI 有助可理解性，但不能替代效能與安全驗證 [11]。

Unresolved Problems：不同使用者是否願以少量預測精度換取更高可解釋度，需要使用者

研究。


爭論 3：自主 Agent vs 規則約束 Agent

A｜自主 Agent 能靈活分解任務並呼叫工具，減少固定流程限制。

B｜規則約束能限制錯誤健康建議和不可靠工具行為。

Evidence / Consensus：環境決策研究認為 LLM 很適合輔助角色而非完全自主決策 [8]。

Unresolved Problems：適當自主層級、低資料品質下的拒答閾值，仍需場景測試。

                                 AIoT-DA · 2026.11.03 · Final Project Proposal

<PARSED TEXT FOR PAGE: 12 / 22>

                                           AIRGUARD AI / FINAL PROJECT PROPOSAL


Q3. 十個深度理解問題（每題附辨識要點）

推理層次        問題                              深入理解的判別要點

            為什麼 PM2.5 當前濃度不等於官方             應指出六種污染物、不同平均
Why
            即時 AQI？                         窗、最大副指標。

            若 API 延遲兩小時，但模型有預測，             應標示過期／降級，不將預測偽
What-if
            Agent 應如何回覆？                    裝成官方即時數據。

            若 XGBoost 比 Persistence 只小幅
                                            應考慮統計不確定性、成本與產
Trade-off   改善 MAE，但延遲更高，怎麼取
                                            品門檻。
            捨？

Failure     為何隨機切分時間序列會使模型成績                應說明時間依賴、未來資訊洩漏

Case        失真？                             與 rolling-origin。

            如何驗證活動建議是否真的遵循環境                需建測試案例、規則對照與人工
Evidence
            部 AQI 指引？                       審核準則。


Comparis    為何 1 小時與 6 小時 PM2.5 預測不         預測難度、誤差分層、不同站點
on          能只看單一 MAE？                      與區間。

Design      為何採取「Agent 規劃、模型計算、             應說明可追溯、可測試、避免

Decision    規則決策」分離？                        LLM 裸估數值。

Real-
            某測站缺值、隔壁站 AQI 正常，能否 應指出空間代表性、不能擅自精
world
            推薦該街區慢跑？                        細插值。
Scenario


Uncertain   若預測區間跨越風險門檻，如何表
                                            應呈現不確定性並採保守判讀。
ty          述？

            SHAP 顯示風速重要，是否可推論風              不能，需區分相關、因果及潛在
Causality
            速造成污染下降？                        混雜。



                                          AIoT-DA · 2026.11.03 · Final Project Proposal

<PARSED TEXT FOR PAGE: 13 / 22>

                                        AIRGUARD AI / FINAL PROJECT PROPOSAL


4. Proposed Scheme / Proposed Design

4.1 Scope、User Scenarios 與 Functional Requirements

 Scenario     輸入            系統行為                      輸出

 S1 早晨跑       臺中、07:00、40   查官方 AQI → PM2.5 1–        建議時段、趨勢、來

 步            分鐘、一般族群       6h 預測 → 比較時段              源與風險

 S2 敏感族       指定站點、敏感族      官方 AQI 規則優先；若不
                                                      風險說明與適用限制
 群            群、戶外活動        確定採保守輸出

 S3 資料異       資料過期／API 失    檢查 freshness；使用可          缺漏告知、不作假即

 常            效             用歷史資料或降級                  時判斷




4.2 System Architecture（①–⑧ 必須編號）




            圖 1. AirGuard AI 八個編號模組；②–⑧ 執行可追溯的資料與決策流程。

① User / Web UI：收集查詢、位置、活動類型、時間與一般／敏感族群設定。

② Query Interpreter：解析意圖、時間與監測站；要求缺失的重要參數。


                                       AIoT-DA · 2026.11.03 · Final Project Proposal

<PARSED TEXT FOR PAGE: 14 / 22>

                                               AIRGUARD AI / FINAL PROJECT PROPOSAL

③ Planner & Reasoning Agent：規劃工具呼叫，限制外部工具種類與呼叫次數。

④ Data Acquisition：讀取環境部 AQI 即時 API、歷史 CSV 與本地快取；檢驗更新時間。

⑤ Analytics Engine：特徵工程、1/3/6h PM2.5 預測、估計誤差及解釋。

⑥ Domain Knowledge Integration：校驗官方 AQI 規則、族群活動建議、日期與風險表

述。

⑦ Decision / Recommendation：根據資料和規則比較時段，不輸出醫療診斷。

⑧ Output & Interaction：顯示來源、資料時間、預測趨勢、限制與可檢視的決策軌跡。


4.3 Flowchart（含 Decision、Exception）




     圖 2. Input → Planner → Retrieval → 資料品質 Decision → ML → Domain Rules →

                          Recommendation → Output。



                                              AIoT-DA · 2026.11.03 · Final Project Proposal

<PARSED TEXT FOR PAGE: 15 / 22>

                                                AIRGUARD AI / FINAL PROJECT PROPOSAL


4.4 Data Acquisition、Schema 與 Target

  Layer / Source     實際欄位與用途                                      頻率／限制

                                                                  官方頁面註明每小
  AQX_P_432（即        SiteId, SiteName, AQI, PM2.5, PM10, O3,
                                                                  時；可能延遲／缺
  時）                 publishtime；顯示官方即時狀態
                                                                  值

                                                                  每小時資料；按月
  AQX_P_488（歷        SiteId, DataCreationDate, PM2.5,
                                                                  份下載；依欄位完
  史）                 WindSpeed 等；歷史分析與回測輔助
                                                                  整性檢驗

                     SiteId, ItemName, ItemUnit,                  每小時觀測、每日
  AQX_P_13（歷史
                     MonitorDate, MonitorValue00…23；建模 更新；須將寬表轉
  污染物）
                     主資料                                          長表

                                                                  2025 年起門檻修
  Domain rules       MOENV 即時 AQI 副指標與活動建議
                                                                  正；需記錄版本



建模目標 y_(station,t+h) = PM2.5 原始每小時濃度（μg/m³），h ∈ {1,3,6}；輸入只使用預

測時間 t 可取得的歷史／當下資料（lag 1, 3, 6, 12, 24 小時、rolling stats、hour-of-day、

weekday、可能的風速等）。官方 AQI 狀態與預測 PM2.5 為不同輸出，不直接用 PM2.5 估

成完整未來 AQI。

研究區域：以臺中市有足夠歷史資料的官方測站為首批試點；測站名單將於資料品質盤點後

確定。假設下載 2024–2026 年的可用資料，但實際時間覆蓋、缺值比例及 API 限額仍待工

程確認。


4.5 Pseudocode｜Algorithm 1：Evidence-Grounded Agent

Algorithm 1 AirGuardAgent(Q, user_context) → Response

01 request ← parse_intent(Q, user_context)


                                               AIoT-DA · 2026.11.03 · Final Project Proposal

<PARSED TEXT FOR PAGE: 16 / 22>

                                                      AIRGUARD AI / FINAL PROJECT PROPOSAL

02 assert request.location and request.time_window

03 plan ← planner.select_tools(request, allowed_tools)

04 live ← retrieve_official_aqi(plan.station)

05 hist ← retrieve_recent_pm25(plan.station)

06 quality ← validate(site_id, timestamps, units, missingness)

07 if quality.is_stale or quality.is_insufficient:

08   return safe_fallback(quality, official_link, no_live_claim)

09 latest_aqi ← live.official_aqi # NOT model output

10 features ← build_past_only_features(hist, cutoff=now)

11 forecasts ← model.predict(features, horizons=[1,3,6])

12 uncertainty ← estimate_error_bands(forecasts, station)

13 rules ← lookup_official_activity_rules(latest_aqi, request.group)

14 evidence ← assemble(live, forecasts, uncertainty, rules)

15 candidates ← evaluate_activity_windows(request, evidence)

16 decision ← conservative_rank(candidates, uncertainty, rules)

17 response ← compose_with_citations(decision, evidence)

18 response ← guardrail_check(response, timestamp, scope, policy)

19 if not response.passed: response ← safe_fallback(...)

20 log_audit(request, plan, evidence, response)

21 return response


4.6 Pseudocode｜Algorithm 2：Time-Safe Forecasting

Algorithm 2 TrainAndEvaluate(station_hourly_data)

01 D ← load_and_standardize_units(station_hourly_data)

02 D ← sort_by(station_id, observation_time)

03 D ← mark_invalid_and_missing(D)

04 for h in [1,3,6]:

05   X_h ← lag_and_rolling_features(D, cutoff=t)

06   y_h ← observed_pm25_at(t + h)


                                                     AIoT-DA · 2026.11.03 · Final Project Proposal

<PARSED TEXT FOR PAGE: 17 / 22>

                                                    AIRGUARD AI / FINAL PROJECT PROPOSAL

07   train, valid, test ← chronological_split(X_h, y_h)

08   baseline ← persistence(train, horizon=h)

09   candidates ← [Ridge, RandomForest, XGBoost]

10   tune_on_rolling_origin(candidates, train, valid)

11   best ← select_by_valid_MAE_and_operating_cost()

12   freeze(best); pred ← best.predict(test.X)

13   compare_to_baseline(pred, baseline, MAE, RMSE)

14   stratify_by_station_horizon_pollution_episode()

15   calibrate_prediction_intervals(valid_residuals)

16   report_CI_ablation_failure_cases_and_provenance()

17 return versioned_models_and_evaluation_report


4.7 Implementation Mapping & Technical Feasibility

  Component      預計技術與責任                                            可測試接口

                 React / Next.js：情境表單、預測圖表、來源卡                      query_form /
  Frontend
                 片                                                  result_view

  Agent          Python FastAPI + LLM Function Calling；tool         POST

  Service        allowlist                                          /agent/query

                 MOENV API adapter、CSV
  Data Service                                                      GET /stations, /aqi
                 ETL、SQLite/PostgreSQL cache

  ML Service     scikit-learn / XGBoost、版本化預測模型                     POST /forecast

  Knowledge                                                         evaluate_activity(
                 官方 AQI 規則 JSON + 來源版本；可選 RAG
  Layer                                                             aqi,group)


  Evaluation &                                                      tests/ +
                 pytest、離線 backtesting、案例集、人工覆核
  QA                                                                experiments/




                                                  AIoT-DA · 2026.11.03 · Final Project Proposal

<PARSED TEXT FOR PAGE: 18 / 22>

                                                  AIRGUARD AI / FINAL PROJECT PROPOSAL

API 風險：如官方 API 要求憑證或有頻率限制，先以官方 CSV 快取展示；如 LLM API 無法

使用，保留 deterministic planner / rules 作為降級方案，不讓完整展示依賴單一付費服

務。



5. Experiments & Evaluation Plan｜實驗與評估設計

5.1 Dataset、Split 與 Data Quality Protocol

   資料覆蓋：優先使用 2024–2026 年可取用的臺中市官方監測資料；先產出測站與時間覆

    蓋率表，再確認樣本期間。

   嚴格時序：按觀測時間建立 train／validation／test（預計 70/15/15），再用 rolling-

    origin 檢驗對不同月份／季節的泛化。

   避免洩漏：特徵只使用 t 時刻已發布之資料；所有 rolling windows 都依時間往過去展

    開；避免以 t+h 已知數值造特徵。

   資料品質：統計缺失率、延遲、異常值比例，並呈現資料保留／剔除原則、時間戳及臺

    灣時區。


5.2 Baselines、Models 與 Metrics

    類型              比較方案                                      指標

    Forecast        Persistence y(t+h)≈y(t)；Seasonal Naive    MAE、RMSE、skill vs

    baseline        y(t+h)≈y(t+h−24h)                         baseline

                    Ridge、Random Forest、XGBoost；視資            分時距、分測站、分污
    Classical ML
                    源可加 LSTM                                  染級別誤差


    Explainabilit                                             解釋合理性、穩定性
                    SHAP 特徵解釋與部分案例人工檢視
    y                                                         （定性／量化）




                                                 AIoT-DA · 2026.11.03 · Final Project Proposal

<PARSED TEXT FOR PAGE: 19 / 22>

                                         AIRGUARD AI / FINAL PROJECT PROPOSAL


    類型         比較方案                                  指標

                                                     工具選擇正確率、來源
    Agent /    Rule-only vs Agent+ML+Rules；正常／缺
                                                     完整率、規則一致率、
    Decision   值／過期／衝突案例
                                                     安全降級率、延遲




5.3 Detailed Evaluation Design

   時間序列回測：使用 1、3、6 小時預測時距，報告相對於 Persistence 的 MAE /

    RMSE；以測站與高污染事件分組，避免平均分數遮蔽嚴重失敗。

   模型比較：固定資料與流程，在 validation 調參，test 只使用一次；對預測誤差及樣本

    數附註信賴區間或 bootstrap。

   Ablation：移除風場特徵、移除不確定性提示、移除規則引擎等，研究其對數值及決策

    品質的影響；不可把 SHAP 直接解讀為因果。

   Agent casebook：設計至少 30 個測試情境（預定數量），涵蓋普通／敏感族群、資料

    過期、同名測站、超範圍地址、模糊時段、無法上網與混淆 AQI／PM2.5 的問題。

   System QA：記錄 Agent 回應時間（P50/P95）、API 失敗降級、輸出來源時間、可重

    現的資料集／模型版本。


5.4 Expected Outcomes & Limitations

預期：在至少部分測站及時距，經適當特徵工程的模型可能優於 Persistence；但若未超越

基線仍應如實報告，重新調整預測範圍。預期 Agent 可依固定情境測試呈現官方資料、模

型結果、限制與活動指引，但效能門檻需根據 Pilot data 設定，不能先宣稱準確率或減少健

康風險。

適用範圍與限制：本系統不提供醫療診斷，不將測站數據等同於街道級個人暴露，也不以模

型 PM2.5 預測取代官方 AQI。模型效能與實際應用價值應由後續實驗驗證。




                                        AIoT-DA · 2026.11.03 · Final Project Proposal

<PARSED TEXT FOR PAGE: 20 / 22>

                                                   AIRGUARD AI / FINAL PROJECT PROPOSAL


6. Implementation Roadmap、Risk & Handover

 工作階段         里程碑（建議）                                驗收證據

              確認 API／CSV、測站、時間範圍、
 W1 資料盤點                                             EDA + data dictionary
              資料品質

              Persistence / Ridge / RF / XGBoost
 W2 預測基線                                             baseline results + notebook
              回測

 W3 Agent 核
              工具呼叫、官方規則及安全降級                         unit tests + agent traces
 心

 W4 Web 整
              情境查詢、圖表、來源卡片                           可操作 demo
 合

 W5 評估強化 消融、30 案例、效能與限制                              evaluation report

 W6 Final     README、DESIGN、PPT、
                                                     交付檢查清單
 Handover     YouTube Demo




主要風險與緩解措施

 Risk                    Mitigation

 開放資料缺值／API 限額           歷史 CSV 快取、Schema 驗證、fallback、告知時間戳。

 模型未超越 naive
                         降階為趨勢描述／規則建議；誠實報告負結果。
 baseline

 資料洩漏／泛化不足               時間切分、rolling-origin、地點／季節分組評估。

 LLM 幻覺與健康建議風            官方規則引擎、來源檢查、禁止個人醫療診斷、human

 險                       review。



                                              AIoT-DA · 2026.11.03 · Final Project Proposal

<PARSED TEXT FOR PAGE: 21 / 22>

                                                    AIRGUARD AI / FINAL PROJECT PROPOSAL


  Risk                       Mitigation

  使用者混淆預測 PM2.5              將官方 AQI 與模型預測分開標示，保留測站、時間、單

  與官方 AQI                    位、來源及不確定性，避免將預測誤述為官方數據。




References｜資料來源與文獻

[1] World Health Organization. (2024). Ambient (outdoor) air pollution.

  https://www.who.int/news-room/fact-sheets/detail/ambient-(outdoor)-air-quality-

  and-health

[2] Ministry of Environment, Taiwan. (2026). Air Quality Management: 2025 air quality

  statistics.

  https://www.moenv.gov.tw/en/env-affairs/atmospheric-environment/air-quality/

  air-quality-management/2673.html

[3] Chianese, E., & Riccio, A. (2026). Air-Quality Forecasting Across Monitoring,

  Predictor, and Validation Regimes. Forecasting, 8(4), 72.

  https://doi.org/10.3390/forecast8040072

[4] Lu, H., & Lu, H. (2026). Leakage-Aware Research Design for Interpretable PM2.5

  Prediction Across Urban Air-Quality Monitoring Sites. Journal of Advanced

  Research Design, 141(1), 329–340.

  https://akademiabaru.com/submit/index.php/ard/article/view/6838

[5] 環境部環境資料開放平臺。AQX_P_432：空氣品質指標(AQI)（每小時）。

  https://data.moenv.gov.tw/dataset/detail/AQX_P_432

[6] 環境部環境資料開放平臺。AQX_P_488：空氣品質指標(AQI)（歷史資料）。

  https://data.moenv.gov.tw/dataset/detail/AQX_P_488

[7] 環境部環境資料開放平臺。AQX_P_13：空氣品質監測小時值資料（每日更新）。

  https://data.moenv.gov.tw/dataset/detail/AQX_P_13



                                                   AIoT-DA · 2026.11.03 · Final Project Proposal

<PARSED TEXT FOR PAGE: 22 / 22>

                                                      AIRGUARD AI / FINAL PROJECT PROPOSAL

[8] Nie, Q., & Liu, T. (2025). Large language models: Tools for new environmental

   decision-making. Journal of Environmental Management, 375, 124373.

   https://doi.org/10.1016/j.jenvman.2025.124373

[9] Gao, K., et al. (2025). Instructor–Worker large language model system for policy

   recommendation: A case study on air quality analysis of the January 2025 Los

   Angeles wildfires. International Journal of Applied Earth Observation and


   Geoinformation, 143, 104774. https://doi.org/10.1016/j.jag.2025.104774

[10] Joseph, F. J. J., & Ganapathy, S. (2025). Role of artificial intelligence and learning

   techniques in time series forecast of PM2.5 data: An extensive review. Franklin

   Open, 13, 100372. https://doi.org/10.1016/j.fraope.2025.100372

[11] Houdou, A., et al. (2024). Interpretable Machine Learning Approaches for

   Forecasting and Predicting Air Pollution: A Systematic Review. Aerosol and Air

   Quality Research, 24, 230151. https://doi.org/10.4209/aaqr.230151

[12] Yao, S., et al. (2023). ReAct: Synergizing Reasoning and Acting in Language

   Models. ICLR. https://arxiv.org/abs/2210.03629

[13] World Health Organization. (2021). WHO global air quality guidelines (PM2.5,

   PM10, O3, NO2, SO2, CO).

   https://www.ncbi.nlm.nih.gov/books/NBK574591/table/ch3.tab26/

[14] 環境部空氣品質監測網。空氣品質指標 AQI 與健康影響及活動建議（2025 起修訂門

   檻）。https://airtw.moenv.gov.tw/cht/Information/Standard/AirQualityIndicatorN

   ew.aspx

[15] Lo, K., et al. (2025). Integrating satellite information, land use regression, and

   machine learning to estimate the spatiotemporal variation of ionic composition in

   PM2.5 across Taiwan. Science of The Total Environment, 994, 180050.

   https://doi.org/10.1016/j.scitotenv.2025.180050




                                                     AIoT-DA · 2026.11.03 · Final Project Proposal
```
