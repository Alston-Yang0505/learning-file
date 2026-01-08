# 114學年度第1學期工程專題

# 一、主題 
## 以棒球棒、桌球拍、羽球拍及高爾夫球桿作為訓練資料類別，利用XnView對照片進行批次轉換，再使用AlexNet及SqueezeNet兩種神經網路進行學習，測試在相同資料數量及訓練參數下，個別的訓練率及最終能正確辨別照片中球具種類。
### AlexNet結構圖 : 
<img width="437" height="191" alt="image" src="https://github.com/user-attachments/assets/a7b9a631-0054-45a3-9fe1-aa984bd74a32" />

### SqueezeNet結構圖:
<img width="342" height="381" alt="image" src="https://github.com/user-attachments/assets/27df313b-e88d-416b-a7ab-e825b5e26c71" />

# 二、收集資料
## 在這次的資料收集中，我蒐集了四種球具的照片，分別為棒球棒、桌球拍、羽球拍及高爾夫球桿，每種球類大約有35張實體照片和15張卡通插畫圖片，為了讓機器學習的訓練資料圖片可以統一且轉為MatLab支援的照片形式，我使用XnView將圖片轉換為jpg檔並設定為全彩，再將檔名統一，更改的檔名盡量以英文命名，並且避免數字開頭，否則容易造成資料讀取失敗。
<img width="726" height="319" alt="image" src="https://github.com/user-attachments/assets/eb16f146-3c7f-47eb-bf58-792bd7cfffee" />

# 三、建立模型挖掘資料
## 首先，在Data區將資料匯入至神經網路中，並設定資料隨機以順逆時針90度之間旋轉及隨機放大1~2倍左右，設定訓練及驗證資料比例為7:3，每種球具的圖片數量均為一致，使訓練結果更穩定。
<img width="498" height="250" alt="image" src="https://github.com/user-attachments/assets/692a4065-a39e-47c0-96b4-29a252de501a" />
<img width="511" height="221" alt="image" src="https://github.com/user-attachments/assets/de7f028f-92be-4d61-a6ae-8d61051be71f" />
<img width="506" height="249" alt="image" src="https://github.com/user-attachments/assets/6f532f7a-1169-4033-b6e6-0e7f22ce876f" />

## 接著到Designer的部分，將最後一層卷積層替換，並將卷積核改為1x1，並將NumFilters依照分類數更改為4，最後將原始的最後一層分類層移除並換上新的分類層，因為原始分類層是針對起初的任務而設定的。
<img width="371" height="333" alt="image" src="https://github.com/user-attachments/assets/928c7b18-4e61-483f-933b-68bfbaeab3da" />

## 最後到Training階段，將學習率設定在0.0001，這是為了避免訓練過快造成結果不穩定的保守數值，將最小批次大小設定為5，整個訓練將會進行8次，驗證頻率為35，用於檢測是否有過擬和的情況。
<img width="364" height="406" alt="image" src="https://github.com/user-attachments/assets/4c6e2d10-08c2-42f2-b671-9af63bf041f3" />

# 四、實驗結果
## SqueezeNet
<img width="719" height="317" alt="image" src="https://github.com/user-attachments/assets/9bfcb4d2-1e91-4b6f-b032-f588477dca14" />

## AlexNet
<img width="720" height="323" alt="image" src="https://github.com/user-attachments/assets/8a0281d7-8105-4599-b8c4-8c6aa35c4f45" />

### 檢測圖片程式碼
```
I = imread("a01");
I = imresize(I, [227 227]);
[YPred,probs] = classify(trainedNetwork_1,I);
imshow(I)
label = YPred;
title(string(label) + ", " + num2str(100*max(probs),3) + "%");
```
# 五、實驗結果討論
## 在兩種神經網路的訓練下，辨別的結果大致為正確的，除了羽球拍都被辨識為桌球拍，可能原因是羽球拍的拍面與桌球拍的形狀較為類似，或者是檢測的羽球拍範例圖背景顏色較與大部分桌球球拍的拍面顏色較為相近，因此被誤認為桌球拍。
## 起初在訓練時，因為無法讀取訓練資料庫導致訓練無法進行，但檢查了訓練參數後，卻沒有發現異常的問題，後賴經過XnView及訓練資料的比對下，發覺有幾張照片是XnView無法成功讀取的，造成批次轉換照片格式時遺漏，進而影響MatLab讀取資料失敗 ，經過刪減及更換照片並重新調整檔案形式後，訓練成功執行。
<img width="299" height="168" alt="image" src="https://github.com/user-attachments/assets/56ef8dcf-b19e-4e6c-b8b7-04b1fc70ee54" />

# 六、心得感想
## 在這次的工程專題中，首先學到了如何使用XnView將多張照片的檔案形式統一，讓照片不用單一張分別處理，耗費大量時間，也能一覽所有照片的格式是否成功轉換，以便快速找到是否有遺漏的照片，這個工具不僅讓機器學習的資料收集更方便，未來生活中也很有幫助，例如報告圖片的處理甚至是生活中相簿的照片整理，都是十分實用的，在實作前，在老師的課程介紹下，我對機器學習的運作及專有名詞有初步的認識，也有利用Techable Machine及課堂中使用攝影機收集照片，了解機器學習的運作模式，也發現當僅有少量的資料數或有模稜兩可的照片角度時，機器學習無法非常精準判斷及分辨，因此在收集資料時，要避免找尋難以辨識的圖片，例如 : 僅有球拍側面的圖片或含有過多不相干元素的背景，接著進入到MatLab，起初在設定訓練參數時，我還不了解許多參數背後的意義，但配合MatLab網站的說明及老師的示範解釋，讓我發現其實參數設定沒有如此死板，只要在合理的範圍內，就可以藉由反覆的實驗下找到最適合的訓練設定，在這次的試驗中，我認為最困難的是找尋及匯入資料的部分，再輸入資料的過程中，看似簡單的步驟，卻有許多需要注意的細節，像是檔名、圖片類型等，甚至在匯入後才發覺照片有重複，或者是無法成功進入MatLab中，就需要反覆核對和檢查是否有照片不合適，在找尋最終的測試照片時，也要避免與訓練資料重複，否則有失檢測的準確性，在這次的專題中，不僅學到了機器學習的過程和各項參數的意義，也學習到照片的預處理，在現今科技發達的時代中，機器學習與現實生活已經密不可分，藉由這次課程，也讓我初步理解平常大家使用的AI的運作概念，希望接下來的課程能學到更多有關人工智慧的知識。

