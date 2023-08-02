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
&emsp;&emsp;為了可以將影像處理的目標更接近於我們感興趣的區域(即超音波影像區域)。如圖(三)，在一般的超音波影像會有診斷資料、使用哪種模式測量等文字。我們找到超音波影像區域的邊緣後，利用遮罩的方式抓出每幀圖像實質為超音波影像區域的位置，如圖(四)。<br/>
<div align=center>
   
   ![圖(三)心臟超音波影像](https://github.com/Sapphire0912/LaboratoryProject/blob/main/%E5%B0%88%E9%A1%8C%E5%B1%95%E8%B3%87%E6%96%99/image/%E5%BF%83%E8%87%9F%E8%B6%85%E9%9F%B3%E6%B3%A2%E5%BD%B1%E5%83%8F.jpg)
   <center>圖(三)心臟超音波影像</center><br><br/>
</div>

<div align=center>
   
   ![圖(四) ROI 範圍](https://github.com/Sapphire0912/LaboratoryProject/blob/main/%E5%B0%88%E9%A1%8C%E5%B1%95%E8%B3%87%E6%96%99/image/ROI%20%E7%AF%84%E5%9C%8D.jpg)
   <center>圖(四) ROI 範圍</center>
</div>

   * 骨架化(圖像細化)  
&emsp;&emsp;為了找到心臟的肌肉區域範圍，該演算法透過迭代掃描圖像，在每次迭代中刪除圖像中的像素，直到圖像停止變化，以便將肌肉的像素寬度減少到1。我們對影像的每幀進行骨架化，最後將每幀的結果疊加，如圖(五)，取得整體影像中最有可能為心臟肌肉的區域。利用此種方法，限制心臟的邊界。在做骨架化(圖像細化)之前，我們除了找到 ROI 範圍外還對影像做了濾波、形態學、二值化的處理，目的是為了避免原始超音波影像模糊導致不容易抓出心臟的肌肉區域。
<div align=center>
   
   ![圖(五) 骨架圖](https://github.com/Sapphire0912/LaboratoryProject/blob/main/%E5%B0%88%E9%A1%8C%E5%B1%95%E8%B3%87%E6%96%99/image/%E9%AA%A8%E6%9E%B6%E5%8C%96%E5%9C%96.jpg)
   <center>圖(五) 骨架圖</center>
</div>

   * 動態閾值  
&emsp;&emsp;由於真實患者超音波影像的數據樣本並非像其他數據庫的樣本清晰。在參考資料[2]的做法，使用 Gray Level Symmetric Axis Transform偵測腔室的區域，接著利用 SVM 及 Constellation 對腔室做語意分析。我們則採用動態閾值方法及 distance transform 來偵測腔室區域，首先在心臟範圍及 ROI 的區域內，收集每一幀中每個像素的灰階值並且繪製成直方圖，觀察每幀的灰階值分布，如圖(六)、圖(七)。根據每一幀採用不同閾值及參數，以達到區分腔室及肌肉區域。
<div align=center>
   
   ![圖(六) 灰階直方圖](https://github.com/Sapphire0912/LaboratoryProject/blob/main/%E5%B0%88%E9%A1%8C%E5%B1%95%E8%B3%87%E6%96%99/image/%E7%81%B0%E9%9A%8E%E7%9B%B4%E6%96%B9%E5%9C%96.jpg)
   <center>圖(六) 灰階直方圖</center><br><br/>
</div>

<div align=center>
   
   ![圖(七) 不同幀灰階直方圖](https://github.com/Sapphire0912/LaboratoryProject/blob/main/%E5%B0%88%E9%A1%8C%E5%B1%95%E8%B3%87%E6%96%99/image/%E4%B8%8D%E5%90%8C%E5%B9%80%E7%9A%84%E7%81%B0%E9%9A%8E%E7%9B%B4%E6%96%B9%E5%9C%96.jpg)
   <center>圖(七) 不同幀灰階直方圖</center>
</div>

   ※ 註：詳細的演算法計算在 [N06-Tutorial Multi-Threshold 教學文件][src]

   [src]: <https://github.com/Sapphire0912/LaboratoryProject/blob/main/N06-Tutorial/Multi-Threshold%20%E6%95%99%E5%AD%B8%E6%96%87%E4%BB%B6.pptx>
   
   * 圖像分割  
&emsp;&emsp;根據 Apical four chamber view，我們使用了動態閾值得到了初步腔室的範圍後，為了定義每幀的每個腔室及瓣膜位置，採取了統計的方法。由於在瓣膜打開的時間，瓣膜位置在影像上較模糊，不容易區分心房和心室的範圍，因此我們先統計整個影像的腔室位置，接著再利用機器學習模型訓練，得到每個腔室具體的位置，如圖(八)。
<div align=center>
   
   ![圖(八) 腔室語意分析](https://github.com/Sapphire0912/LaboratoryProject/blob/main/%E5%B0%88%E9%A1%8C%E5%B1%95%E8%B3%87%E6%96%99/image/%E8%85%94%E5%AE%A4%E8%AA%9E%E6%84%8F%E5%88%86%E6%9E%90.jpg)
   <center>圖(八) 腔室語意分析</center><br><br/>
</div>

   * 定義瓣膜位置  
&emsp;&emsp;利用骨架圖以及腔室語意分析的結果，定義二尖瓣位置。我們採用基於規則的做法，初步定義二尖瓣支點的位置，如圖(九)，限制了左心室(Left Ventricle)的範圍，以供計算左心室射血分數(Left Ventricular Ejection Fraction)以及定義左心室肌肉區段的語意分析使用。
<div align=center>
   
   ![圖(九) 定義二尖瓣支點](https://github.com/Sapphire0912/LaboratoryProject/blob/main/%E5%B0%88%E9%A1%8C%E5%B1%95%E8%B3%87%E6%96%99/image/%E5%AE%9A%E7%BE%A9%E4%BA%8C%E5%B0%96%E7%93%A3%E6%94%AF%E9%BB%9E.jpg)
   <center>圖(九) 定義二尖瓣支點</center><br><br/>
</div>

   * 左心室肌肉區段語意分析  
&emsp;&emsp;根據 Apical four chamber view的心臟結構以及醫學對於左心室上肌肉區段的定義如圖(十)，主要有六個區段 basal septal、septal、apical septal、apical lateral、lateral 和 basal lateral。我們利用二尖瓣位置和動態閾值方法，將超音波影像中左心室肌肉區域和醫學定義的位置做匹配，接著將每個區段重新取樣，得到結果如圖(十一)。
<div align=center>
   
   ![圖(十) A4C 模型圖](https://github.com/Sapphire0912/LaboratoryProject/blob/main/%E5%B0%88%E9%A1%8C%E5%B1%95%E8%B3%87%E6%96%99/image/Apical%20Four%20Chamber%20%E6%A8%A1%E5%9E%8B%E5%9C%96.jpg)
   <center>圖(十) Apical Four Chamber 模型圖</center><br><br/>
</div>

綠點為 apical septal、藍點為 septal、紅點為 basal septal、天空藍點為 apical lateral、黃點為 lateral、粉色點為 basal lateral。

<div align=center>
  
   ![圖(十一) 左心室肌肉區段語意分析圖](https://github.com/Sapphire0912/LaboratoryProject/blob/main/%E5%B0%88%E9%A1%8C%E5%B1%95%E8%B3%87%E6%96%99/image/%E5%B7%A6%E5%BF%83%E5%AE%A4%E8%82%8C%E8%82%89%E5%8D%80%E6%AE%B5%E8%AA%9E%E6%84%8F%E5%88%86%E6%9E%90%E5%9C%96.jpg)
   <center>圖(十一) 左心室肌肉區段語意分析圖</center>
</div>

</details>

<details>
   <summary id="result_present"> 成果展示 </summary>
   ※ 註：在這裡直接展示結果影片
   
   > ![Segment_case_00004042](https://github.com/Sapphire0912/LaboratoryProject/blob/main/N04-TestReport/Segment/00004042_110428_0999.avi)
</details>

<details>
   <summary> 結論與未來展望 </summary>

   * 結論  
&emsp;&emsp;我們正在構建一個全自動且可擴展的心臟超音波影像分析系統，其中包含圖像分割、辨識 view 和結構測量，分析包括心房、心室和心肌在內的心臟部分，以及彩色都卜勒診斷血液是否逆流。列出這些心臟結構的量測值，輔助醫生收集所有的症狀，例如：二尖瓣閉鎖不全、三尖瓣閉鎖不全、主動脈閉鎖不全、左心室舒張期受損(心臟衰竭)等。<br><br/>
   * 未來展望  
&emsp;&emsp;目前我們最優先的目標是計算左心室射血分數來評估心臟功能是否正常。由於醫生在評估心臟功能時，不會只看患者的其中一個 View 就直接做診斷，還會採取 apical long axis、apical two chamber。為了更接近醫生診斷的結果，因此接下來會分析上述 View。近年來，醫學有較新的診斷左心室功能的技術，global longitudinal strain，此項技術在超音波影像上，除了需要做肌肉區段的語意分析外，也需要計算心臟在收縮及舒張時的收縮率，未來會朝著該方向繼續發展。
</details>

<details>
   <summary> 參考資料 </summary>
   
   [1]	https://www.ahajournals.org/doi/epub/10.1161/CIRCULATIONAHA.118.034338  
   [2]	S. Ebadollahi; Shih-Fu Chang; H. Wu (2004, July). Automatic View Recognition in Echocardiogram Videos using Parts-Based Representation. Proceedings of the 2004 IEEE Computer Society Conference on Computer Vision and Pattern Recognition, 2004. CVPR 2004, Washington, DC, USA.  
   [3]	https://dicom.innolitics.com/ciods/us-image  
</details>
