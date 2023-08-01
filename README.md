# LaboratoryProject 資料夾內容說明
* [專題展資料](#independent_study)
    * [專題內容快速瀏覽](#study_browser)
    * [實踐方法](#implement)
    * [成果展示](#result_present) 
* [實驗室專案](#lab_project)
    * [G01-SourceCode](#source_code)
    * [N01-API](#api)
    * [N02-Architecture](#architecture)
    * [N03-DevelopmentLog](#develop_log)
    * [N04-TestReport](#test_report)
    * [N05-Release](#release)
    * [N06-Tutorial](#tutorial)


※ 註：實驗室專案的資料是由校方教師和醫生合作取得，具有保密協定。因此在 N03-DevelopmentLog、N04-TestReport 僅擺放允許展示的資料。
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
1.  為了診斷特定疾病及降低誤判率，達到輔助醫生做出最佳診斷。
2.  不同角度的超音波影像，針對影像的心臟結構定義腔室及肌肉的位置和範圍。
3.  透過與醫生討論，此系統的目標是計算 Apical four chamber view 的 LVEF。
4.  左心室的定義和範圍及二尖瓣位置是首要條件。
</details>

<details>
   <summary> 工作流程 & 系統架構 </summary>

&emsp;&emsp;主要流程分別分為醫院、醫生和系統。關於此系統，我們使用計算機視覺的演算法對心臟結構進行分類並分析測量結果。與其他系統的不同之處在於，我們並沒有使用來自其他資料庫的樣本，而是從醫生獲取患者的心臟超音波影像，真實患者的超音波影像並不像其他資料庫的樣本清晰，我們希望此系統能夠為患者帶來更低的成本，使得可以負擔起個人數據採集和跟蹤系統。
 
<div align=center>
   
   ![圖(一)工作流程圖](https://github.com/Sapphire0912/LaboratoryProject/blob/main/%E5%B0%88%E9%A1%8C%E5%B1%95%E8%B3%87%E6%96%99/image/%E5%B7%A5%E4%BD%9C%E6%B5%81%E7%A8%8B%E5%9C%96.jpg)
   <center>圖 (一) 工作流程圖</center><br><br/>
   
<div align=center>
   
   ![圖(二)系統架構圖](https://github.com/Sapphire0912/LaboratoryProject/blob/main/%E5%B0%88%E9%A1%8C%E5%B1%95%E8%B3%87%E6%96%99/image/%E7%B3%BB%E7%B5%B1%E6%9E%B6%E6%A7%8B%E5%9C%96.JPG)
   <center>圖 (二) 系統架構圖</center>
   
</details>

<details>
   <summary id="implement"> 實踐方法 </summary>  

**※ 註：每個超音波原始圖像的大小為 800 * 600 pixel**

   * 心臟超音波影像敘述  
&emsp;&emsp;心臟超音波已是醫生常用來檢查心臟相關疾病的工具，利用超音波探測物體的距離及大小。在診斷期間，將超音波的探頭放置在患者胸部上方並發射音波，接觸到心臟再反射由探頭接收，進而描繪心臟的影像。心臟超音波通常與都卜勒超音波和彩色都卜勒結合，以評估通過心臟瓣膜的血流。經過不同角度的超音波檢查，可以提供血管及各部分構造更詳細的資訊，可以檢視心臟的大小、收縮情形，進而評估心臟功能是否正常。不同角度的超音波又稱為 View，每個 View 會根據超音波探頭的位置和穿過心臟斷層平面的方向來定義名稱。我們常用的有五種 view，分別是 parasternal long axis、parasternal short axis、apical four chamber、apical two chamber 和 apical long axis。<br><br/>

   * 影像預處理  
&emsp;&emsp;為了可以將影像處理的目標更接近於我們感興趣的區域(即超音波影像區域)。如圖(三)，在一般的超音波影像，會有診斷資料、使用哪種模式測量等文字。我們找到超音波影像區域的邊緣後，利用遮罩的方式抓出每幀圖像實質為超音波影像區域的位置，如圖(四)。<br/>

<div align=center>
   
   ![圖(三)心臟超音波影像](https://github.com/Sapphire0912/LaboratoryProject/blob/main/%E5%B0%88%E9%A1%8C%E5%B1%95%E8%B3%87%E6%96%99/image/%E5%BF%83%E8%87%9F%E8%B6%85%E9%9F%B3%E6%B3%A2%E5%BD%B1%E5%83%8F.jpg)
   <center>圖(三)心臟超音波影像</center><br><br/>
</div>

<div align=center>
   
   ![圖(四) ROI 範圍](https://github.com/Sapphire0912/LaboratoryProject/blob/main/%E5%B0%88%E9%A1%8C%E5%B1%95%E8%B3%87%E6%96%99/image/ROI%20%E7%AF%84%E5%9C%8D.jpg)
   <center>圖(四) ROI 範圍</center>
</div>

   * 動態閾值
   * 圖像分割
   * 定義瓣膜位置
   * 左心室肌肉區段語意分析     
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
