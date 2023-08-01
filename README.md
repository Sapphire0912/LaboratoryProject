# LaboratoryProject 資料夾內容說明
* [專題展資料](#independent_study)
    * [專題內容快速瀏覽](#study_browser)
* [實驗室專案](#lab_project)
    * [G01-SourceCode](#source_code)
    * [N01-API](#api)
    * [N02-Architecture](#architecture)
    * [N03-DevelopmentLog](#develop_log)
    * [N04-TestReport](#test_report)
    * [N05-Release](#release)
    * [N06-Tutorial](#tutorial)


※ 註：實驗室專案的資料是由校方教師和醫生合作取得, 具有保密協定。因此在 N03-DevelopmentLog、N04-TestReport 僅擺放允許展示的資料。
* * *  

<h2 id="independent_study"><br>專題展資料<br/>專題題目: 心臟超音波影像之肌肉語意區段偵測與腔室範圍估計改良</h2> 
<h3 id="study_browser"> 專題內容快速瀏覽 </h3>
<details>
   <summary> 摘要 </summary>
   
&emsp;&emsp;根據世界衛生組織統計，心血管疾病是全球的第一大死因，估計每年奪去 1790 萬人的生命。近年來，超音波的技術有了極大的進步，可以對心臟結構和功能進行評估。心臟超音波的發展可以詳細的顯示人體在正常生理狀態和病理狀態的心臟結構、測量和功能的系列檢查，透過此項技術提高了診斷的準確性。基於與醫生合作的經驗，我們創建了這個醫療項目，使用超音波影像來描繪心肌、瓣膜、腔室，建立一個分析心臟結構測量的系統。這些計算方法，我們 _**基於規則的系統 (rule-based system)**_ 對心臟每個部分進行分類並儲存測量值以供將來機器學習訓練。該系統用於支持連續患者的跟蹤、分析心臟超音波影像，診斷特定疾病降低誤判率，幫助醫生以做出最佳診斷，提高醫療品質。 _**通過與醫生討論，我們列出了疾病及其症狀，開發了一個系統來分析心臟的量測值，以檢測不同類型的疾病**_。
</details>

<details>
   <summary> 研究動機 & 目的 </summary>

&emsp;&emsp;由於心血管疾病一直位於全球十大死因的榜首，直到心臟超音波技術的發展針對心臟結構的評估及測量，使得提高了醫生診斷的準確性。為了診斷特定疾病及降低誤判率，幫助醫生做出最佳診斷，我們採取影像處理的技術對心臟超音波影像進行分析，在不同角度的心臟超音波影像，針對該影像的心臟結構定義腔室及肌肉的位置和範圍。透過與醫生討論，我們開發了一個系統來分析心臟的量測值，除了檢測不同類型的疾病外，同時輔助醫生診斷的一個工具。<br/>
&emsp;&emsp;現今許多計算機視覺的演算法，已被用在自動駕駛系統和臉部識別上。為了達到理想的結果，這些演算法在計算時都需要大量的數據樣本，然而
_**我們採用基於規則的系統，針對心臟的每個部份進行分類，再給予機器學習模型訓練，即使沒有大量的數據也可以達到理想的成果**_。
* 以下條列式敘述研究目的：
1.  A
2.  B
3.  C
4.  D
</details>

<details>
   <summary> 工作流程 </summary>
</details>

<details>
   <summary> 實踐方法 </summary>  
   
   1. 影像預處理    
   2. 動態閾值    
   3. 圖像分割    
   4. 定義瓣膜位置    
   5. 左心室肌肉區段語意分析     
</details>

<details>
   <summary> 成果展示 </summary>
</details>

<details>
   <summary> 結論與未來展望 </summary>
</details>

<details>
   <summary> 參考資料 </summary>
</details>
