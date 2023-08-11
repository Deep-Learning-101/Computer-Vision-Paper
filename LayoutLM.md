# LayoutLM
Paper: [LayoutLM: Pre-training of Text and Layout for Document Image Understanding](https://arxiv.org/pdf/1912.13318.pdf)

Authors: Yiheng Xu,Minghao Li, Lei Cui, Shaohan Huang, Furu Wei, Ming Zhou

Public: arXiv:1912.13318, 2020


[github](https://github.com/microsoft/unilm/tree/master/layoutlm)

[論文筆記](https://zhuanlan.zhihu.com/p/166128964)
## 　Abstract
Pre-training techniques have been verified successfully in a variety of NLP tasks in recent years. Despite the widespread use of pre-training models for NLP applications, they almost exclusively focus on text-level manipulation, while neglecting layout and style information that is vital for document image understanding. In this paper, we propose the **LayoutLM** to jointly model interactions between text and layout information across scanned document images, which is beneficial for a great number of real-world document image understanding tasks such as information extraction from scanned documents. Furthermore, we also leverage image features to incorporate words' visual information into LayoutLM. To the best of our knowledge, this is the first time that text and layout are jointly learned in a single framework for document-level pre-training. It achieves new state-of-the-art results in several downstream tasks, including form understanding (from 70.72 to 79.27), receipt understanding (from 94.02 to 95.24) and document image classification (from 93.07 to 94.42).

在近年來，預訓練技術在多種自然語言處理（NLP）任務中取得了成功。儘管預訓練模型在NLP應用中被廣泛使用，但它們幾乎僅專注於文本層級的操作，忽略了版面和風格信息，而這些對於文檔圖像理解至關重要。

因此，提出了一種名為LayoutLM的模型，它能夠在掃描文檔圖像中共同建模文本和版面信息之間的交互作用，這對於許多現實世界的文檔圖像理解任務（如從掃描文檔中提取信息）非常有益。此外，該論文還利用圖像特徵將文字的視覺信息融入到LayoutLM中。

值得注意的是，這是首次在單一框架中聯合學習文本和版面的文檔層級預訓練。該模型在幾個下游任務上取得了新的最先進結果，包括表格理解（從70.72%提高到79.27%）、收據理解（從94.02%提高到95.24%）和文檔圖像分類（從93.07%提高到94.42%）等。

總的來說，LayoutLM的提出填補了NLP預訓練模型忽略版面和風格信息的空白，並在文檔圖像理解領域取得了重要的突破和成果。

## Introduction

1. 理解商業文件是一項非常具有挑戰性的任務。有些公司通過耗時且昂貴的人工登打工作從商業文件中提取數據，同時需要手動定制或配置。

2. 目前的文件分析方法通常基於深度神經網絡，早期的嘗試通常專注於檢測和分析文件的某些部分，如表格區域。[7] 是首先提出基於卷積神經網絡（CNN）的PDF文件表格檢測方法。此後，[21、24、29] 也利用更先進的Faster R-CNN模型[19]或Mask R-CNN模型[9]來進一步提高文件版面分析的準確性。此外，[28] 提出了一種端到端、多模態、完全卷積網絡，從文件圖像中提取語義結構，充分利用來自預訓練自然語言處理模型的文本嵌入。最近，[15] 提出了一種基於圖卷積網絡（GCN）的模型，以結合文本和視覺信息，用於文件人工智慧領域。
3. 但這樣的方法，有兩個限制：
(1) They rely on a few human-labeled training samples
without fully exploring the possibility of using large-scale unlabeled training samples. 
(2) They usually leverage either pre-trained　CV models or NLP models, but do not consider a joint training of　textual and layout information. Therefore, it is important to investigate how self-supervised pre-training of text and　layout may help　in the document AI area

* 提出的方法 LayoutLM，一種簡單而有效的文本和佈局預訓練方法，用於文檔圖像理解任務。受 BERT 模型[4]的啟發，輸入文本信息主要由文本嵌入和位置嵌入表示，LayoutLM 進一步添加了兩種類型的輸入嵌入：（1）二維位置嵌入，表示文檔中標記的相對位置； (2) 將掃描的令牌圖像嵌入到文檔中。 LayoutLM的架構如圖2所示。
![Alt text](<./images/Screenshot from 2023-07-21 16-31-28.png>)

##  EXPERIMENTS
### Pre-training Dataset

* 預訓練模型的性能很大程度上取決於數據集的規模和質量。
* 在 IIT-CDIP Test Collection 1.0 上進行了預訓練，其中包含超過 600 萬份文檔，其中包含超過 1100 萬張掃描文檔圖像。此外，每個文檔都有其相應的文本和元數據存儲在 XML 文件中。文本是對文檔圖像應用OCR產生的內容。元數據描述文檔的屬性，例如唯一標識和文檔標籤。儘管元數據包含錯誤和不一致的標籤，但這個大型數據集中的掃描文檔圖像非常適合預訓練我們的模型

### Fine-tuning Dataset
***FUNSD 數據集***。我們在 FUNSD 數據集上評估我們的方法，以理解嘈雜的掃描文檔中的形式。該數據集包括 199 個真實的、完全註釋的掃描表單，其中包含 9,707 個語義實體和 31,485 個單詞。這些形式被組織為相互鏈接的語義實體列表。每個語義實體包括唯一標識符、標籤（即問題、答案、標題或其他）、邊界框、與其他實體的鏈接列表以及單詞列表。數據集分為 149 個訓練樣本和 50 個測試樣本。我們採用詞級F1分數作為評價指標。
We adopt the ***word-level F1 score*** as the evaluation metric.

### Task-Specific 

Receipt Understanding. This task requires filling several predefined semantic slots according to the scanned receipt images. For instance, given a set of receipts, we need to fill specific slots ( i.g., company, address, date, and total). Different from the form understanding task that requires labeling all matched entities and keyvalue pairs, the number of semantic slots is fixed with pre-defined keys. Therefore, the model only needs to predict the corresponding values using the sequence labeling method.

資料標註時,需要標註 公司, 地址, 日期, 金額

## Result
Form Understanding. We evaluate the form understanding task on the FUNSD dataset. The experiment results are shown in Table 1. We compare the LayoutLM model with two SOTA pre-trained NLP models: BERT and RoBERTa [16]. The BERT BASE model achieves 0.603 and while the LARGE model achieves 0.656 in F1. Compared to BERT, the RoBERTa performs much better on this dataset as it is trained using larger data with more epochs. Due to the time limitation, we present 4 settings for LayoutLM, which are 500K document pages with 6 epochs, 1M with 6 epochs, 2M with 6 epochs as well as 11M with 2 epochs. It is observed that the LayoutLM model substantially outperforms existing SOTA pre-training baselines. With the BASE architecture, the LayoutLM model with 11M training data achieves 0.7866 in F1, which is much higher than BERT and RoBERTa with the similar size of parameters. In addition, we also add the MDC loss in the pre-training step and it does bring substantial improvements on the FUNSD dataset. Finally, the LayoutLM model achieves the best performance of 0.7927 when using the text, layout, and image information at the same time. In addition, we also evaluate the LayoutLM model with different data and epochs on the FUNSD dataset, which is shown in Table 2. For different data settings, we can see that the overall accuracy is monotonically increased as more epochs are trained during the pre-training step. Furthermore, the accuracy is also improved as more data is fed into the LayoutLM model. As the FUNSD dataset contains only 149 images for fine-tuning, the results confirm that the pre-training of text and layout is effective for scanned document understanding especially with low resource settings.
| 1|2 |
| :----: | :----: |
|![Alt text](<./images/Screenshot from 2023-07-21 17-03-59.png>) |![Alt text](<./images/Screenshot from 2023-07-21 17-04-21.png>)|

##   CONCLUSION 
We present LayoutLM, a simple yet effective pre-training technique with text and layout information in a single framework. Based on the Transformer architecture as the backbone, LayoutLM takes advantage of multimodal inputs, including token embeddings, layout embeddings, and image embeddings. Meanwhile, the model can be easily trained in a self-supervised way based on large scale unlabeled scanned document images. We evaluate the LayoutLM model on three tasks: form understanding, receipt understanding, and scanned document image classification. Experiments show that LayoutLM substantially outperforms several SOTA pre-trained models in these tasks. For future research, we will investigate pre-training models with more data and more computation resources. In addition, we will also train LayoutLM using the LARGE architecture with text and layout, as well as involving image embeddings in the pre-training step. Furthermore, we will explore new network architectures and other self-supervised training objectives that may further unlock the power of LayoutLM.