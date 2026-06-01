---
layout: default
title: 2026 電腦視覺資源懶人包 (Computer Vision) | YOLO, OCR & Diffusion | Deep Learning 101
description: 2026 電腦視覺 (CV) 開源模型選型指南。收錄 YOLOv11、AOI 異常檢測、高精度 OCR (DeepSeek/MinerU)、Stable Diffusion 影片生成與免標註圖像分割等工業級視覺實戰資源。
permalink: /Computer-Vision
lang: zh-Hant
schema_type: service
service_type: AI Consulting
---

{% include header.html %}

---

# 👁️ 電腦視覺 (CV)・必讀資源總整理

> **編者按：** 本頁面彙整了電腦視覺領域的關鍵技術資源，涵蓋物件偵測、生成式 AI、影像分割以及文字識別（OCR）等最新論文與實作。
>
> 如果您想尋找更詳細的筆記，歡迎訪問 **GitHub Repository**：
> 👉 [**GitHub: Computer-Vision-Paper**](https://github.com/Deep-Learning-101/Computer-Vision-Paper) (歡迎 Star ⭐)


{% include ai-share.html %}

---

### **文章目錄**
- [Anomaly Detection (異常檢測)](#anomalydetection)
- [Object Detection (目標偵測)](#objectdetection)
- [Segmentation (圖像分割)](#segmentation)
- [OCR (光學文字識別)](#ocr)
- [Diffusion Model (擴散模型)](#diffusion-model)
- [Digital Human (虛擬數字人)](#digital-human)

---

### 👁️ 2026 全球電腦視覺開源模型大全：YOLO 家族與擴散模型 (Diffusion)

#### 1\. Object Detection (目標偵測與 YOLO 生態系)

*目標偵測的標準幾乎由 YOLO 家族定義。此區塊整理了目前最主流的 YOLO 版本與新世代開放詞彙（Open-Vocabulary）模型。特別標註開發源頭，方便針對地緣資安需求進行選型。*

**A. 國際大廠與台灣原生強權 (資安合規首選)**

| 模型名稱 | 開發團隊 | 💡 核心優勢與突破點 | 🚀 推薦場景 & 規格標籤 |
| :--- | :--- | :--- | :--- |
| **YOLOv11** | 🇺🇸 **Ultralytics** | **全能視覺霸主**。架構大翻新，不僅做目標偵測，還原生支援實例分割、姿態辨識與旋轉邊界框 (OBB)。 | 邊緣運算、多任務視覺 AI<br>`[歐美開源]` `[多任務支援]` |
| **YOLOv9** | 🇹🇼 **中研院 (王建堯博士團隊)** | **台灣之光！** 導入 PGI (Programmable Gradient Information) 技術，解決深層網路資訊遺失問題，參數少但準確度極高。 | 資源受限的本地端設備、瑕疵檢測<br>`[台灣開發]` `[高參數利用率]` |
| **YOLOv8** | 🇺🇸 **Ultralytics** | **生態系最完善**。雖然不是最新，但在社群中的教學、部署套件、ONNX/TensorRT 轉換資源最為豐富。 | 工業級穩定部署、初學者專案<br>`[生態豐富]` `[極易部署]` |
| **OV-DINO** | 🇺🇸 **國際學術界** | **開源工業開放詞彙目標檢測**。不需要預先定義好類別，直接用自然語言提示 (Prompt) 就能找出畫面中對應的物體。 | 零樣本 (Zero-shot) 偵測、通用場景<br>`[Open-Vocabulary]` `[前沿技術]` |

* **[ViCrop-Det](https://arxiv.org/abs/2604.26806)** `[2026-04-29]` 🔥
  * **核心優勢**：**打破小目標檢測的算力魔咒，首創「免訓練、即插即用」的空間注意力熵 (SAE) 智能裁剪框架。** 這款由華中科技大學提出的神作，巧妙利用 DETR 檢測器內建的交叉注意力分布作為「內生探針」，透過計算香農熵精準揪出模型「不確定且重要」的區域（即小目標藏身處）進行局部高解析度重檢測。僅需微幅增加約 20% 計算量，即可在 VisDrone 數據集上穩定提升近 3 個百分點的 mAP，以極高的推理幀率 (38.6 FPS) 徹底碾壓 SAHI 等暴力全圖切片方法。
  * **解決痛點 / 推薦場景**：**完美解決了 Transformer 檢測器在密集場景中「注意力被空曠背景稀釋導致微小目標蒸發」，以及傳統 SAHI 切片法「計算量線性暴增」的致命痛點。** 由於無需重新訓練且不更動網路架構，極度適合企業直接掛載於現有模型上，部署於**無人機航拍 (UAV) 密集微小物件偵測**、**自駕車遠距離行人辨識**，以及**衛星遙感影像大圖分析**等計算資源受限但需極高精度的邊緣運算場景。<br>`[免訓練即插即用]` `[小目標檢測]` `[碾壓SAHI]` `[邊緣運算首選]`
  * **資源**：[🐙 GitHub (待釋出搜尋)](https://github.com/search?q=ViCrop-Det+Hui+Wang+HUST) | [📄 論文](https://arxiv.org/abs/2604.26806) | [📝 深度解讀](https://mp.weixin.qq.com/s/UQZENPtcQ-M2AiQu41OKcg)

* **[FS-DETR](https://github.com/YT3DVision/FSDETR)** `[2026-04-21]` 🔥 `[小目標偵測]` `[頻域空間融合]` `[邊緣運算]`
  * **核心優勢**：**打破極端小目標漏檢魔咒，首創「頻域-空間」雙軌融合的輕量級檢測神作！** 基於 RT-DETR 架構進行深度魔改，創新引入二維快速傅立葉變換 (FFT2D) 提取高頻紋理，並結合空間層次注意力 (SHAB) 與可變形稀疏採樣 (DA-AIFI)。在參數僅有 14.7M（比 RT-DETR-R18 瘦身 26%）的極致輕量化條件下，仍能精準捕捉僅數十像素的微小物體，小目標檢測效能 (APₛ) 強勢輾壓 D-Fine-M 與 RT-DETRv2。
  * **解決痛點 / 推薦場景**：**完美解決了傳統 YOLO/DETR 在邊緣設備上「縮小模型就嚴重漏檢、做大模型又跑不動」，以及全局注意力容易被密集背景雜訊干擾的致命痛點。** 實測在 VisDrone (高密度交通) 與 TinyPerson (極端低對比度微小行人) 等嚴苛資料集上創下 SOTA。是打造**無人機高空巡檢 (UAV)**、**衛星遙感影像分析**，以及部署於算力極限**邊緣運算盒子 (Edge AI)** 的工業級首選。
  * **資源**：[🐙 GitHub 官方開源](https://github.com/YT3DVision/FSDETR)

**B. 亞洲/中國頂尖開源 (極致效能與端側特化)**

| 模型名稱 | 開發團隊 | 💡 核心優勢與突破點 | 🚀 推薦場景 & 規格標籤 |
| :--- | :--- | :--- | :--- |
| **YOLOv10** | 🇨🇳 **清華大學** | **徹底消滅 NMS**。首次在 YOLO 家族中移除後處理的非極大值抑制 (NMS)，大幅降低推理延遲。 | 即時自動駕駛、無人機視覺<br>`[無後處理]` `[超低延遲]` |
| **VisionReasoner** | 🇨🇳 **開源社群** | **統一視覺感知與推理**。利用強化學習技術，標榜效能可對標 Qwen2.5-VL 等大型視覺模型。 | 複雜場景理解、視覺問答<br>`[強化學習]` `[大模型對標]` |
| **MCL** | 🇨🇳 **AAAI 2025** | **遙感影像專家**。專為空拍、衛星圖設計的半監督目標檢測框架 (Multi-clue Consistency Learning)。 | 農業監測、空拍圖分析<br>`[遙感特化]` `[半監督學習]` |

-----

#### 2\. Diffusion Model & Video Generation (影像生成與擴散模型)

*影像生成已從單純的「文生圖 (Text-to-Image)」進化到「影片生成 (Video Generation)」與「精準控制」。本區塊區分歐美主流開源底座與亞洲大廠的高效能模型。*

**A. 國際主流底座與生態系 (設計與產能主力)**

| 模型/工具名稱 | 開發團隊 | 💡 核心優勢與突破點 | 🚀 推薦場景 & 規格標籤 |
| :--- | :--- | :--- | :--- |
| **Flux 系列** | 🇩🇪 **Black Forest Labs** | **Stable Diffusion 的真正繼承者**。目前最強大的開源生圖模型，提供 Canny/Depth/Fill 等強大控制網開發工具。 | 專業 AI 繪圖、高質量商稿生成<br>`[開源王者]` `[極致細節]` |
| **Sana** | 🇺🇸 **NVIDIA / MIT 等** | **比 FLUX 快 100 倍！** (ICLR 2025 Oral)。導入新一代架構，大幅降低生成高清圖片所需的算力與時間。 | 實時圖像生成、低算力設備<br>`[極速生成]` `[NVIDIA加持]` |
| **ComfyUI Impact Pack** | 🌐 **國際開源社群** | **最強臉部修復擴充**。ComfyUI 生態系中必裝的節點包，專治 AI 生成的人物臉部崩壞或手部變形問題。 | 人像生成、細節修補工作流<br>`[ComfyUI外掛]` `[必裝工具]` |
| **FramePack** | 🌐 **國際開源社群** | **低顯存影片生成神器**。能在 6G 顯存下跑 13B 模型，最高支援生成 1 分鐘的長影片。 | 個人創作者影片生成、低階顯卡<br>`[6G顯存]` `[長影片]` |

**B. 亞洲/中國開源大模型 (影片生成與實用工具)**

| 模型/工具名稱 | 開發團隊 | 💡 核心優勢與突破點 | 🚀 推薦場景 & 規格標籤 |
| :--- | :--- | :--- | :--- |
| **Wan-Video (萬相)** | 🇨🇳 **阿里巴巴** | **全模態、全尺寸影片生成**。阿里萬相大模型開源，具備極強的物理規律理解與高解析度影片生成能力。 | 影視特效預覽、廣告素材生成<br>`[大廠開源]` `[全尺寸]` |
| **HunyuanVideo-I2V** | 🇨🇳 **騰訊** | **高質量圖生影片**。開源了圖生視訊模型以及專屬的 LoRA 訓練腳本，客製化彈性極高。 | 動態插畫、個人化風格影片<br>`[支援LoRA]` `[圖生影片]` |
| **Phantom** | 🇨🇳 **字節跳動** | **10G 顯存可用**。支援生成 1280x720 高清影片的模型，硬體門檻相對友善。 | 社交媒體短影音、720P生成<br>`[低硬體門檻]` `[字節跳動]` |
| **HivisionIDPhotos** | 🇨🇳 **開源社群** | **智慧證件照生成神器**。全自動完成精準摳圖、換背景、裁切任意尺寸，實用性極高。 | 攝影工作室、自動化影像處理<br>`[超高實用性]` `[一鍵生成]` |
| **Index-AniSora** | 🇨🇳 **Bilibili (B站)** | **二次元特化**。B 站開源的 SOTA 動畫影片生成模型，對動漫風格的掌握度目前無人能出其右。 | 動畫製作輔助、二次元創作<br>`[動漫風格]` `[SOTA模型]` |

---

## AnomalyDetection
**🏭 Anomaly Detection (工業異常檢測與 AOI)**

傳統 AOI (自動光學檢測) 高度依賴大量瑕疵樣本來訓練模型。但在真實工業場景中，收集數千張「特定種類」的瑕疵圖往往不切實際。近年來，異常檢測技術已轉向**少樣本 (Few-shot)** 與 **零樣本 (Zero-shot)** 學習。以下為 2025-2026 年最具代表性的開源方案：

### 1. 結合 LLM 與多模態的零樣本檢測 (Zero-shot AD)
利用大語言模型或 CLIP 龐大的常識庫，在「沒看過瑕疵樣本」的情況下，直接透過文字描述或視覺特徵揪出異常。

* **[JUDO](https://github.com/woodavid31/JUDO)** `[2026-05]` 🔥
  * **核心優勢**：**打破通用大模型產線翻車魔咒，首創「對照式定位＋領域知識內化＋GRPO 推理對齊」的工業異常多模態推理器。** 這款 ICLR 2026 頂會神作基於 Qwen2.5-VL-7B 打造，徹底拋棄外掛 RAG 容易引發幻覺與邏輯偏離的弱點。它透過輸入「正常標準件與待檢件」進行視覺並置對照 (SegJux)，將工業質檢標準深植於模型權重 (DomInj)，並利用多層獎勵函數 (GRPO) 嚴格約束空間定位與工藝邏輯。在 MMAD 基準測試中，以 81.20% 的平均準確率強勢擊敗 GPT-4o。
  * **解決痛點 / 推薦場景**：**完美解決了傳統視覺大模型 (VLM) 在工業現場「看得出異常，卻給不出符合工藝邏輯的解釋」的致命痛點。** 它的輸出不再只是模糊的「合格/不合格」，而是能精準定位缺陷並解釋對裝配或密封的影響，讓 AI 推理真正可被人工複核。極度適合企業用來建構**次世代 AOI 瑕疵問答系統**、**自動化品質工程追溯 (SPC) 流程**，以及**產線專家級決策輔助大腦**，打通工業質檢的最後一哩路。<br>`[產線質檢大腦]` `[GRPO推理對齊]` `[超越GPT-4o]`
  * **資源**：[🐙 GitHub](https://github.com/woodavid31/JUDO) | [📄 論文](https://arxiv.org/abs/2605.20284) | [📝 深度解讀](https://mp.weixin.qq.com/s/7WFnkb-Vp9euyzkGLqDS2g)

* **[DCS (DINO-CLIP-SAM)](https://doi.org/10.3390/app16041836)** `[2026-06]` 🔥
  * **核心優勢**：**集結三大視覺基礎模型之大成，無需任何瑕疵樣本即可達成像素級精準分割的零樣本檢測王牌！** 這套發表於 MDPI 的創新框架，將 Grounding DINO（候選定位）、CLIP（語義感知）與 SAM（精細分割）完美串聯且完全凍結骨幹權重。透過引入細粒度文本提示 (FinePrompt)、雙路徑跨模態交互 (ADCI) 修銳異常熱力圖，以及「框＋正負點」提示組合器 (BPPC)，徹底補平了大模型間的語義斷層。在 MVTec-AD 與 VisA 基準上分別創下 94.6% 與 97.2% AUROC 的零樣本極致表現。
  * **解決痛點 / 推薦場景**：**完美解決了傳統工業質檢「異常樣本極度稀缺」，以及單純使用 CLIP/SAM 進行零樣本預測時「邊界模糊、語義歧義嚴重」的致命痛點。** 由於具備強大的開放詞彙 (Open-vocabulary) 泛化能力，極度適合**高頻換線的柔性製造產線 (High-Mix Low-Volume)**、**缺乏歷史瑕疵數據的新品試產期 (NPI) AOI 檢測**，以及作為**雲端/離線高精度瑕疵複判大腦**（需注意其串聯三大模型帶來的算力開銷，不建議用於極低延遲的邊緣設備）。<br>`[零樣本AOI]` `[大模型串聯]` `[像素級分割]` `[免微調骨幹]`
  * **資源**：[🐙 GitHub (社群實作搜尋)](https://github.com/search?q=DCS+Zero-Shot+Anomaly+Detection+DINO+CLIP+SAM) | [📄 論文](https://doi.org/10.3390/app16041836) | [📝 深度解讀](https://mp.weixin.qq.com/s/OaLdkHD1s4iQnBh-qAL3yA)

* **[LLM2CLIP](https://microsoft.github.io/LLM2CLIP/)** `[2026-01-29]` 🔥
  * **核心優勢**：微軟開源黑科技！結合大語言模型 (LLM) 強大的常識推理能力來增強 CLIP 模型的視覺表徵。
  * **解決痛點**：完美解決了傳統 CLIP 在遇到罕見工業瑕疵或長尾分佈數據時容易誤判的問題，非常適合用於高精度的零樣本瑕疵檢測。[📄 AlphaXiv 論文](https://www.alphaxiv.org/abs/2411.04997) | [📝 公眾號深度解讀](https://mp.weixin.qq.com/s/-U03e1KZmFCoXTGzdYbC0Q)

* **[AA-CLIP](https://deepwiki.com/Mwxinnn/AA-CLIP)** `[2025-04-12]`：透過 Anomaly-Aware 機制增強 CLIP 的零樣本異常檢測能力。

* **[AnomalyCLIP](https://deepwiki.com/zqhang/AnomalyCLIP)** `[2025-04-27]`：Object-agnostic Prompt Learning，實現跨物體的零樣本異常偵測。

* **[AdaptCLIP](https://github.com/aiiu-lab/AdaptCLIP)** `[2025-05-15]`：將 CLIP 模型適配為通用的視覺異常檢測器。

* **[Multi-Modal LLM for AD (VELM)](https://deepwiki.com/Sassanmtr/VELM)** `[2025-05-05]`：不僅偵測異常，還能進行分類與動作建議的工業多模態架構。

* **[OneNIP](https://github.com/gaobb/OneNIP)** `[2024-10]` 🔥
  * **核心優勢**：**終結產線「海量瑕疵數據」焦慮，單張正常圖片即插即用的全科質檢神醫！** 這款收錄於 ECCV 2024 的重磅開源神作，徹底打破傳統 AOI 必須「收集海量缺陷、專病專治」的成本高牆。透過首創的「單一正常圖像提示 (Normal Image Prompt)」與「雙向交叉注意力 (Bidirectional Cross-Attention)」機制，讓模型學會直接與「標準答案（正常件）」進行像素級對照，成功繞過自監督重建網路常見的「身份捷徑 (Identity Shortcut)」陷阱，在 MVTec 與 VisA 等權威工業基準上實現跨類別的 SOTA 表現。
  * **解決痛點 / 推薦場景**：**完美解決了高良率產線「瑕疵樣本極難收集」與「新品上線需重新訓練模型」的致命痛點。** 只要提供一張無瑕疵的黃金樣本 (Golden Sample)，模型就能精準抓出邊緣模糊或具偽裝性的複雜瑕疵，並透過監督式精化器 (Refiner) 輸出高精度的像素級定位。極度適合用於**高頻換線的柔性製造產線 (High-Mix Low-Volume)**、**極少數目缺陷的精密電子 AOI 檢測**，以及企業建構**跨產品線的統一視覺質檢基座**。<br>`[單樣本質檢]` `[AOI神器]` `[跨類別通用]`
  * **資源**：[🐙 GitHub](https://github.com/gaobb/OneNIP) | [📄 論文](https://csgaobb.github.io/Pub_files/ECCV2024_OneNIP_CR_Full_0725_Mobile.pdf)

### 2. 少樣本與無監督學習前沿突破 (Few-shot & Unsupervised)
解決現場只能取得「正常良品圖」或極少量瑕疵圖的痛點。

* **[MeDS](https://github.com/SirojbekSafarov/MeDS)** `[2026-05]` 🔥
  * **核心優勢**：**打破工業質檢「訓練集必須絕對乾淨」的不可能假設，首創無懼 40% 髒數據污染的自清洗抗噪異常檢測框架！** 這篇 ICML 2026 的強悍之作直擊產線最痛的「標籤噪聲」現實。透過「自舉稀疏記憶庫 (Bootstrapped Memory) 粗篩」、「記憶分數蒸餾 (Score Distillation) 細化定位」與「漸進式樣本選擇 (Progressive Selection) 閉環微調」三步法，讓模型自己學會過濾異常。在 MVTecAD 基準測試中，即便訓練集混入高達 40% 的瑕疵樣本，它依然能將 I-AUROC 從崩潰邊緣的 87.38% 強勢拉回 99.16%，展現驚人的魯棒性。
  * **解決痛點 / 推薦場景**：**完美解決了真實工廠中因「輕微缺陷漏標、加工紋理波動、多人標註口徑不一」導致模型決策邊界變寬容、上線後漏檢率飆升的致命痛點。** 它並非要取代現有的 UAD 模型 (如 Dinomaly)，而是作為一層可插拔的「抗污染保險層」掛載於現有架構上。極度適合**數據維護與清洗成本極高的傳統製造業**、**特徵變異大的機加工/鑄造/焊接產線**，以及作為**協助 QC 工程師優先篩檢可疑髒數據的自清洗前置模組**。<br>`[工業抗噪神作]` `[無懼髒數據]` `[自清洗閉環]` `[產線落地首選]`
  * **資源**：[🐙 GitHub](https://github.com/SirojbekSafarov/MeDS) | [📄 論文](https://arxiv.org/abs/2605.26676)

* **[DINO-AD](https://arxiv.org/abs/2602.03870)** `[2026-02]` 🔥
  * **核心優勢**：**打破模型微調成本高牆的免訓練 (Training-Free) 異常檢測黑科技！** 徹底拋棄針對特定資料集重新訓練的繁瑣流程，直接利用凍結的 DINO-V3 自監督視覺特徵，結合首創的「嵌入相似性匹配 (ESM)」與「前景感知 K-means 聚類」。完全零訓練開銷，卻在醫療影像 (Brain/Liver) 的像素級異常檢測上雙雙突破 98% AUROC，強勢輾壓 PatchCore 與 PaDiM 等經典無監督算法。
  * **解決痛點 / 推薦場景**：**完美解決了傳統 AOI 與醫療分析中「異常樣本極度稀缺」以及「每次更換檢測物體都需耗時重新煉丹 (重訓模型)」的致命痛點。** 其多中心聚類設計能完美適應正常組織的自然形態變化，避免過度敏感導致的誤判。極度適合用於**高精度的醫療影像病灶快速篩查**、需要頻繁切換產線的**工業 AOI 柔性製造**，以及算力不允許進行模型訓練的**邊緣運算設備 (Edge AI)**。
  * **資源**：[📄 官方論文 (ISBI 2026)](https://arxiv.org/abs/2602.03870) | *註：官方 2D 實現源碼待釋出，可先參考相關的 3D 異常檢測庫 [DINO3D-AD*](https://github.com/alivecat05/DINO3D-AD)
  `[免訓練 SOTA]` `[無監督學習]` `[醫療影像特化]`

* **[SubspaceAD (YOLO + SubspaceAD 雙引擎架構)](https://github.com/CLendering/SubspaceAD)** `[CVPR 2026]` 🔥 `[1-shot 極限檢測]` `[免訓練]` `[零漏檢架構]`
  * **核心優勢**：**打破 AOI 部署門檻，僅需 1 張良品圖即可實現未知缺陷的免訓練檢測，結合 YOLO 將漏檢率暴降 96%！** 由埃因霍溫理工大學於 CVPR 2026 提出的極簡美學神作。徹底拋棄複雜的記憶庫與提示學習，利用凍結的 DINOv2 提取特徵並擬合 PCA 低維子空間，藉由計算重建殘差精準定位異常。1-shot 設定下，MVTec-AD 圖像級 AUROC 高達 98.0%。
  * **解決痛點 / 推薦場景**：**完美解決傳統 AOI「樣本稀缺、未知缺陷無法識別、換線成本極高」的三座大山。** 透過「有監督 YOLO (抓已知) + 無監督 SubspaceAD (抓未知)」的互補雙引擎，每個品類模型不到 1MB。新品上線只需拍一張正常照片即刻完成部署，導入週期縮短 80%。是**多樣少量生產線質檢**、**資源受限邊緣運算設備**與**快速換線 AOI 系統**的工業級完美解決方案。
  * **資源**：[🐙 GitHub](https://github.com/CLendering/SubspaceAD) | [📄 論文](https://arxiv.org/abs/2602.23013)

* **[SynSur](https://arxiv.org/abs/2604.26633)** `[CVPR 2026]` 🔥 `[合成資料生成]` `[端到端 AOI 管線]` `[LoRA微調]`
  * **核心優勢**：**打破工業瑕疵資料稀缺魔咒，首創「生成即標註」的端到端 AOI 管線！** SynSur 提出一套創新的工作流：利用 VLM 生成瑕疵描述，再透過 LoRA 微調的擴散模型搭配 Mask 引導進行局部瑕疵修復生成，最後透過 DreamSim 與 CLIPScore 自動過濾低質樣本並自動標註。這套一體化流程讓生成樣本的品質直接受檢測模型效能驗證，達成協同優化。
  * **解決痛點 / 推薦場景**：**完美解決了工業產線中「嚴重瑕疵（如刮痕、裂紋）發生率極低，導致模型無法收斂」的致命痛點。** 實測在真實瑕疵樣本極少（如 10 張）的極限場景下，混入 SynSur 生成的合成資料可讓 YOLO 模型的 mAP 提升 3~5 個百分點。非常適合用於**新產品早期質檢**、**罕見瑕疵模型補強**，以及缺乏人力進行標註的**自動化 AOI 系統開發**。
  * **資源**：[📄 論文](https://arxiv.org/abs/2604.26633) | *[官方程式碼尚未開源，但可基於 Hugging Face 的 `StableDiffusionInpaintPipeline` 快速復現]*

* **[One-to-Normal](https://www.alphaxiv.org/abs/2502.01201)** `[2025-06-13]`
  * **核心優勢**：提出 Anomaly Personalization (異常個人化) 概念，在少樣本異常識別上取得重大突破。[📝 中文解讀](https://zhuanlan.zhihu.com/p/1916799842879018831)

* **[DualAnoDiff (CVPR 2025)](https://www.alphaxiv.org/abs/2408.13509v3)** `[2025-06-06]`
  * **核心優勢**：復旦與騰訊優圖實驗室合作入選 CVPR 2025。利用雙向相互關聯的擴散模型，進行少樣本異常圖像生成，以補足工業訓練數據的短板。

* **[CostFilter-AD](https://github.com/ZHE-SAPI/CostFilter-AD)** `[2025-07-16]`：透過 Matching Cost Filtering 技術，刷新無監督異常檢測的效能上限。[📝 中文解讀](https://zhuanlan.zhihu.com/p/1928870223529882075)

* **[Dinomaly](https://github.com/guojiajeremy/Dinomaly)** `[2025-03-25]`：The Less Is More Philosophy，極簡架構的多類別無監督異常檢測方案。

* **[PaDim](https://deepwiki.com/xiahaifeng1995/PaDiM-Anomaly-Detection-Localization-master)** `[2025-04-26]`：工業界極為經典且泛用性高的無監督異常檢測與定位演算法。

### 3. 架構融合與跨模態對齊 (Cross-Architecture Alignment)
* **[MOCHA](https://www.alphaxiv.org/zh/overview/2509.14001v1)** `[2025-09-20]`：Multi-modal Objects-aware 架構。將此技術注入 YOLO 後，檢測效能獲得大幅度成長。[📝 中文解讀](https://zhuanlan.zhihu.com/p/1952054591035281418)
* **[FS-SAM2](https://zread.ai/fornib/FS-SAM2)** `[2025-09-24]`：將 Meta 的 SAM 2 (Segment Anything 2) 模型適配於少樣本語義分割任務，在效能與效率上達到雙優。

---

## ObjectDetection
**🎯 Object Detection (目標偵測)**

目標偵測不僅是畫出邊界框 (Bounding Box)，目前的趨勢是結合語言模型與強化學習，實現「開放詞彙 (Open-Vocabulary)」與「極端場景特化」。

* **[AFSS (Anti-Forgetting Sampling Strategy)](https://arxiv.org/abs/2603.17684)** `[2026-03]` 🔥
  * **核心優勢**：**打破 YOLO 系列「每輪看全量資料」的吃算力魔咒，零侵入性讓訓練速度狂飆 1.6 倍且精度無損！** 這篇 CVPR 2026 的強悍之作，不改 Backbone、不碰 Loss、不影響推論端 (部署零成本)。它首創將「學習充分度 (min(P, R))」作為內生探針，動態把訓練圖分為難/中/易三檔，結合「抗遺忘回看 (Continuous Review)」與「短期覆蓋 (Short-Term Coverage)」機制。讓 GPU 算力精準砸在「模型還沒學好」的困難樣本上，在 COCO 上讓 YOLO11s 訓練時間從 43.9 小時暴降至 28.4 小時。
  * **解決痛點 / 推薦場景**：**完美解決了企業在龐大自定義資料集上訓練時「GPU 算力成本極度高昂」與「中後期訓練邊際效益嚴重遞減」的致命痛點。** 由於完全不干擾原始網路架構，極度適合需要頻繁新增資料、高頻迭代模型的**自駕車感知系統**、**高頻換線的工業 AOI 瑕疵檢測**，以及所有受限於算力預算（如單卡/雙卡開發者）但渴望快速驗證迭代的企業 AI 團隊。<br>`[訓練加速神器]` `[無損提速]` `[抗遺忘採樣]` `[算力省長]`
  * **資源**：[🐙 GitHub (社群實作搜尋)](https://github.com/search?q=Does+YOLO+Really+Need+to+See+Every+Training+Image+in+Every+Epoch) | [📄 論文](https://arxiv.org/abs/2603.17684) | [📝 深度解讀](https://mp.weixin.qq.com/s/tQAlP7UmAsWT-bZLHQDaAA)

* **[EUPE: DINOv3 + SAM + CLIP 三模合一輕量檢測框架](https://github.com/little51/dinov3-samples)** `[2026]` 🔥
  * **核心優勢**：**打破大模型落地門檻的開箱即用神器，將 DINOv3、SAM 與 CLIP 的跨域超能力濃縮進極致輕量的檢測管線！** 基於 Meta 最新的 EUPE (Efficient Universal Perception Encoder) 骨幹，透過 `lightly-train` 框架高度封裝。開發者完全無需從頭煉丹，短短 10 行 Python 程式碼即可直接呼叫在 COCO 資料集上訓練完成的任務頭 (Task Head)，實現精準的開箱即用目標偵測。
  * **解決痛點 / 推薦場景**：**完美解決了傳統視覺大模型 (Vision Foundation Models) 「整合困難、需要手寫複雜下游任務頭」的致命痛點。** 官方貼心釋出從 `ConvNeXt-Tiny` 到 `ViT-Base` 等多種尺寸的預訓練權重。極度適合需要在**邊緣運算設備 (Edge AI)** 快速部署街景分析，或是缺乏算力但想享受 SOTA 級通用視覺特徵的個人開發者與中小企業。
  * **資源**：[🐙 GitHub 完整視覺化實戰源碼](https://github.com/little51/dinov3-samples) | [📄 官方框架說明](https://pypi.org/project/lightly-train)
  `[開箱即用]` `[輕量化部署]` `[三模合一]` `[極簡API]`

* **[Roboflow Trackers](https://github.com/roboflow/trackers)** `[2026]` 🔥 `[多目標跟蹤 MOT]` `[隨插即用]` `[Apache 2.0可商用]`
  * **核心優勢**：**解救演算法工程師的 MOT 隨插即用神器，一行程式碼無縫接軌任意檢測模型！** 徹底打破過去跟蹤演算法與特定檢測器深度耦合、官方程式碼難以魔改的泥淖。內建 SORT、ByteTrack (高低置信度雙階段關聯) 與 OC-SORT (抗遮擋霸主) 等主流演算法。高度模組化設計，只要你的模型（YOLO, RT-DETR 等）能吐出檢測框與置信度，它就能接手產出具備唯一 ID 的連續軌跡。
  * **解決痛點 / 推薦場景**：**完美解決了傳統跟蹤演算法「換個檢測模型就要重寫底層」以及「論文程式碼難以落地」的致命痛點。** 原生支援 CLI 指令，一鍵即可無腦處理本地視訊、攝影機或 RTSP 串流，並內建標準 HOTA 效能評估工具。極度適合需要快速部署**安防監控即時串流分析**、**高動態體育賽事轉播 (SportsMOT)**，以及**自駕車與機器人視覺**等工業級即時追蹤場景。
  * **資源**：[🐙 GitHub 官方開源](https://github.com/roboflow/trackers) | [📄 官方完整文件](https://trackers.roboflow.com) | [🌐 瀏覽器線上 DEMO](https://huggingface.co/spaces/Roboflow/Trackers)

* **[FT-FSOD (Parallel Decoder)](https://github.com/Intellindust-AI-Lab/FT-FSOD)** `[CVPR 2026]` 🔥 `[跨域少樣本]` `[並行解碼器]` `[自動化微調]`
  * **核心優勢**：**打破跨域微調的過度擬合魔咒，僅靠輕量解碼器魔改與漸進式微調，強勢輾壓 SAM 3！** 論文證實，面對巨大域偏移（如工業瑕疵、醫療影像），一味把模型做大是錯的！透過首創的「混合集成解碼器 (HED)」引入並行預測多樣性，搭配 plateau-aware 漸進式微調策略，幾乎**零額外參數**即可徹底解決少樣本訓練極易震盪與收斂困難的致命缺陷。
  * **解決痛點 / 推薦場景**：**完美解決傳統視覺模型導入特殊產業（如工業 AOI 缺陷、空拍圖、水下探勘或文件解析）時，因「標註資料極少」加「場景差異過大」導致模型泛化能力直接崩潰的痛點。** 實測在包含 100 個極端異構資料集的 RF100-VL 基準上，10-shot 效能 (41.9 mAP) 顯著擊敗 SAM 3 與 DINO 家族。極度適合沒有海量算力與標註人力、不想手動痛苦調參，卻需要讓 AI 快速適配陌生新場景的企業級跨域目標檢測任務。
  * **資源**：[🐙 GitHub 官方開源](https://github.com/Intellindust-AI-Lab/FT-FSOD)

* **[Rex-Omni](https://rex-omni.github.io/)** `[CVPR 2026]` 🔥 `[檢測一切]` `[GRPO強化學習]` `[Qwen2.5-VL底座]`
  * **核心優勢**：**打破語言理解與視覺定位的壁壘，首創引入 GRPO 強化學習的「檢測一切」多模態大模型！** 基於 3B 輕量級 Qwen2.5-VL 打造，徹底拋棄傳統 YOLO/DETR 依賴的座標迴歸（Regression），將目標偵測、OCR、GUI 定位與關鍵點提取，全部霸氣統一為「離散座標序列預測」任務。透過獨創的幾何感知獎勵函數（GRPO）進行後訓練，精準糾正了以往多模態模型（MLLM）常見的座標漂移與重複預測問題。
  * **解決痛點 / 推薦場景**：**完美解決了傳統視覺大模型「看得懂複雜指令，卻框不準精確位置」的致命痛點。** 它的零樣本 (Zero-shot) 檢測效能直接匹敵甚至超越 Grounding DINO 等專用模型。極度適合用於開發需要深度語言理解的**自動化 GUI 網頁操作代理 (Web Agent)**、**複雜圖表/排版的 OCR 系統**，以及支援自然語言指令的**開放詞彙 (Open-Vocabulary) 機器人視覺感知系統**。
  * **資源**：[🐙 專案首頁與程式碼](https://rex-omni.github.io/) | [📄 arXiv 論文](https://arxiv.org/abs/2510.12798)

* **[OV-DINO](https://github.com/wanghao9610/OV-DINO)** `[2025-07-24]`
  * **核心優勢**：開源工業開放詞彙目標檢測框架。不需要預先標註所有類別，只需輸入自然語言，模型就能自動找到對應的物體。[📝 中文解讀](https://mp.weixin.qq.com/s/gLAVYFAH_39gT4XC0zWN0A)

* **[CountVid](https://www.alphaxiv.org/abs/2506.15368)** `[2025-06-18]`
  * **解決痛點**：突破傳統模型只能數「特定訓練類別」的限制，支援在動態影片中透過提示詞實現「指哪數哪」的開放世界計數。適合交通車流監控與生產線良率計算。[📝 中文解讀](https://mp.weixin.qq.com/s/hICrrfEgriyktoIxnbjPEQ)

* **[MCL (AAAI 2025)](https://github.com/facias914/sood-mcl)** `[2025]`
  * **解決痛點**：專為無人機空拍圖與衛星遙感影像設計的半監督框架。透過多線索一致性學習，只需極少量標註，就能在超大解析度影像中精準框出微小物件。[📝 中文解讀](https://zhuanlan.zhihu.com/p/26788012528)


* **[VisionReasoner](https://github.com/dvlab-research/VisionReasoner)** `[2025-05-23]`：用強化學習統一視覺感知與推理，對標大廠 VLM。

* **[GeoPix](https://github.com/Norman-Ou/GeoPix)** `[2025-06-15]`：像素級遙感多模態大模型。[📝 實驗室介紹](https://3slab.pku.edu.cn/info/1026/2121.htm)

* **[Falcon](https://deepwiki.com/TianHuiLab/Falcon)** `[2025-03-14]`：遙感視覺與語言基礎模型 (Remote Sensing VLM)。

---

## Segmentation
**✂️ Segmentation (圖像分割)**

自從 Meta 推出 Segment Anything (SAM) 以來，圖像分割已經進入「提示即分割 (Promptable Segmentation)」的時代。

### 1. SAM 家族與通用分割基石

* **[ConceptSeg-R1](https://github.com/NTU-AI4X/ConceptSeg-R1)** `[2026-05]` 🔥
  * **核心優勢**：**打破 SAM/SAM 3 「只懂標籤、不懂邏輯關係」的語義瓶頸，首創由元強化學習 (Meta-GRPO) 驅動的可提示概念分割框架！** 該神作將「分割概念」分為上下文無關 (CI)、上下文依賴 (CD) 與上下文推理 (CR) 三大層次。透過內建的「捷徑路由器 (Shortcut Router)」，它能將多模態大模型 (MLLM) 複雜的深度邏輯推理狀態，翻譯為 SAM 3 能直接讀取的「隱式概念組 (Implicit Concept Groups)」，讓模型學會從視覺演示中歸納規則，實現真正的跨圖表徵與邏輯演繹。
  * **解決痛點 / 推薦場景**：**完美解決了過往「多模態推理與像素分割間存在語義斷層」，以及傳統模型無法識別「靠環境對比與功能關係」才能定義的目標之致命痛點。** 極度適合企業用來建構**高難度醫療病灶精準定位 (如邊緣模糊的息肉或腫瘤)**、**工業級缺陷動態追蹤與對照**，以及需要強大時空推理能力的**次世代泛用型具身智能 (Embodied AI) 視覺大腦**，強勢推動視覺感知從「找物體」邁向「找概念」的典範轉移。<br>`[概念級分割]` `[超越SAM3]` `[元強化學習Meta-GRPO]` `[醫療與缺陷定位]`
  * **資源**：[🐙 GitHub](https://github.com/NTU-AI4X/ConceptSeg-R1) | [📄 論文](https://arxiv.org/abs/2605.20385) | [🌐 專案主頁](https://ntu-ai4x.github.io/ConceptSeg-R1)

* **[CAFe-DINO (DINO-Soars)](https://github.com/rfaulk/DINO_Soars)** `[2026-05]` 🔥
  * **核心優勢**：**打破遙感分割「密集標註地獄」與「巨大域落差」，首創零遙感微調即稱霸 OVSS 的跨域遷移神作！** 這篇 CVPR 2026 Workshop 的重磅論文，巧妙繞過直接拿 DINOv3 跑遙感圖會「糊成一團」的痛點。其核心在於不重訓骨幹，而是利用「空間去噪＋跨類別推理」的成本聚合網路 (Cost Aggregation Network)，搭配凍結的特徵引導上採樣 (AnyUp)，將 DINOv3 的強大潛在表徵「無損洗淨」後遷移至遙感視角。僅用 COCO-Stuff 的 41 個遙感相關子類進行訓練，便在四個權威基準 (Potsdam, Vaihingen, OEM, LoveDA) 達成平均 56.5% 的 SOTA 表現。
  * **解決痛點 / 推薦場景**：**完美解決了遙感影像 (RS) 領域「標註成本極高」且模型「換個城市就拉胯」的致命痛點。** 由於實現了真正的「零遙感微調」，極度適合資源受限但需處理巨量衛星影像的企業或公部門。是建構**跨城市/跨氣候的全球自動化地表覆蓋製圖**、**災區快速變遷分析**，以及**免標註開詞彙無人機 (UAV) 巡檢系統**的工業級首選。<br>`[零遙感微調]` `[OVSS開詞彙分割]` `[DINOv3魔改]` `[遙感衛星大腦]`
  * **資源**：[🐙 GitHub](https://github.com/rfaulk/DINO_Soars) | [📄 論文](https://arxiv.org/abs/2605.03175) | [📝 深度解讀](https://mp.weixin.qq.com/s/UfkO6YAlBO-vnLhGbNtyhA)

* **[LuoHuaLabel (基於 SAM 3 的智慧標註神器)](https://github.com/luohuabuxiema/LuoHuaLabel)** `[2026]` 🔥
  * **核心優勢**：**徹底解放雙手的資料標註黑科技，以 SAM 3 驅動的次世代視覺標註系統！** 完美整合 Segment Anything 3 (SAM 3) 的強大零樣本 (Zero-shot) 分割能力，捨棄傳統耗時的手繪多邊形。支援「單點極速提取輪廓」與「自然語言提示 (Prompt) 全圖自動打框」。更獨創原生 OBB 旋轉框控制手柄（具備防變形與 360° 平滑旋轉），效能與體驗全面輾壓傳統 Labelme / LabelImg。
  * **解決痛點 / 推薦場景**：**完美解決了電腦視覺專案中「手動標註耗時崩潰」、「傾斜目標難以精準框選」以及「標註格式轉換繁瑣」的三大致命痛點。** 系統內建一鍵訓練/驗證集劃分，並支援 JSON、YOLO (.txt 自動座標歸一化)、XML 等多格式無縫匯出。極度適合用於**無人機遙感影像分析 (Remote Sensing)**、**複雜 OCR 文本檢測**，以及需要快速量產高品質**實例分割 (Instance Segmentation)** 訓練資料的工業級開發團隊。
  * **資源**：[🐙 GitHub 官方源碼](https://github.com/luohuabuxiema/LuoHuaLabel) | [📄 SAM 3 論文 (arXiv:2511.16719)](https://arxiv.org/abs/2511.16719) | [📝 開發者實戰指南](https://blog.csdn.net/weixin_29100927/article/details/158752105)
  `[SAM3驅動]` `[智慧標註神器]` `[OBB旋轉框]` `[零成本開源]`

* **[Falcon Perception](https://github.com/tiiuae/falcon-perception)** `[2026-04-01]` 🔥
  * **核心優勢**：**0.6B 極簡單棧架構，開放詞彙分割強勢幹翻 SAM 3！** TII 團隊革命性力作，徹底拋棄傳統「檢測+分割」的複雜 Pipeline，首創「早融合 + 混合注意力」的單一 Transformer 網路。在密集實例（擁擠場景）得分高達 72.6，遙遙領先 SAM 3 (58.4) 與 Qwen3-VL-30B。
  * **解決痛點 / 推薦場景**：**解決了傳統視覺模型模組堆疊導致的「高延遲、難維護」痛點。** 無需繁瑣的後處理與匈牙利匹配，一步到位完成檢測與理解。非常適合算力受限的邊緣運算設備，或需要處理擁擠場景的高效能應用。
  * **資源**：[🐙 GitHub](https://github.com/tiiuae/falcon-perception) | [📄 論文](https://arxiv.org/abs/2603.27365) | [🌐 線上 Demo](https://vision.falcon.aidrc.tii.ae/)

* **[SAM3-I](https://github.com/debby-0527/SAM3-I)** `[2026-05]` 🔥 `[指令驅動]` `[免大模型代理]` `[部件級分割]`
  * **核心優勢**：**打破 SAM 依賴多模態大模型的硬體枷鎖，1.1B 參數效能強勢輾壓 8.8B 巨獸！** 這項由騰訊微信與頂尖大學聯手發表於 ACL 2026 的黑科技，首創「指令感知級聯適配器 (S-Adapter/C-Adapter)」，讓 SAM3 直接具備理解複雜自然語言（如「用來解渴的東西」而非單純的名詞「杯子」）的能力。不需破壞預訓練權重，即可實現從「單純識物」到「高階邏輯聽令」的進化。
  * **解決痛點 / 推薦場景**：**完美解決傳統 SAM 結合 VLM Agent 時「推論極慢、極吃記憶體、容易產生級聯誤差」的致命痛點。** 特別是在面對「一對多」的複雜場景與極精細的「部件級 (Part-level) 分割」時（如精準分割出「帶有鉻合金排氣管的黑色管子」），其準確度遠超過往 SOTA。極度適合部署於**資源受限的邊緣視覺設備 (Edge AI)**、**高互動性具身智能機器人 (Embodied AI)**，以及需要處理**精細工業/醫療影像的零樣本分割系統**。
  * **資源**：[🐙 GitHub](https://github.com/debby-0527/SAM3-I) | [📄 論文](https://arxiv.org/abs/2512.04585)

* **[Meta SAM 3](https://github.com/facebookresearch/sam3)**
  * **核心優勢**：Meta 官方最新分割一切模型，持續推進零樣本分割的極限。[📝 公眾號解讀](https://mp.weixin.qq.com/s/7uDHXQd1ES2mV4dZFB7VMw)

* **Meta SAM 2 及其變體**：
  * [**Meta SAM 2 官方**](https://ai.meta.com/sam2/) | [📝 60行程式碼微調教學](https://mp.weixin.qq.com/s/YfgYCzvi0cXxOFIfQvE_9w)
  * [**SAM2Long**](https://github.com/Mark12Ding/SAM2Long)：解決 SAM 2 長影片追蹤容易丟失目標的問題，影視特效自動摳圖利器。
  * [**SAM2Point**](https://github.com/ZiyuGuo99/SAM2Point)：將 SAM 2 的能力延伸至 3D 點雲數據，為自駕車光達 (LiDAR) 與 3D 醫學影像帶來零樣本分割能力。
  * [**Grounded SAM 2**](https://github.com/IDEA-Research/Grounded-SAM-2)：結合文字 grounding 技術，在影片中追蹤特定物件。

### 2. 領域特化與多模態分割模型

* **[SAM3-LoRA 醫學影像微調實戰 (ISIC 2018)](https://github.com/little51/dinov3-course)** `[2026]` 🔥
  * **核心優勢**：**打破通用大模型在專業領域「水土不服」的魔咒，6GB 顯存即可實現 SAM3 的極速領域特化！** 針對 SAM3 在醫療影像上零樣本能力低下的問題，捨棄昂貴的全參數訓練，導入 LoRA 技術僅微調 0.43% 的關鍵參數 (Q/V/K/Out)。並創新結合「邊界框 (Bounding Box) 提示詞」自動對齊策略，僅需 1 輪訓練即可將皮膚癌病灶的 Dice 係數由 0.892 暴升至 0.943，大幅提升邊緣輪廓的精準度。
  * **解決痛點 / 推薦場景**：**完美解決了將視覺大模型 (VFM) 導入特殊產業時「缺乏自然語言提示詞」以及「全量微調算力門檻過高 (需 12GB+ 顯存)」的致命痛點。** 此開源管線為開發者提供了標準化的二次開發路徑，後續更可無縫串聯 YOLO 等目標偵測模型，實現「先檢測、後精細分割」的全自動化流水線。極度適合**醫療病灶高精度輔助診斷**、**工業 AOI 複雜瑕疵提取**，以及缺乏龐大 GPU 算力的**個人開發者與學術研究團隊**。
  * **資源**：[🐙 GitHub 完整微調源碼](https://github.com/little51/dinov3-course) | [📝 SAM3 微調技術深度解析](https://blog.csdn.net/little51/article/details/145892552)
  `[SAM3微調]` `[醫療影像特化]` `[低算力救星]` `[LoRA極速煉丹]`

* **[X2SAM](https://github.com/wanghao9610/X2SAM)** `[2026-05]` 🔥 `[圖影大一統]` `[多模態分割]` `[時序一致性]`
  * **核心優勢**：**終結圖像與影片分割割裂的全新範式，單一模型包辦 14 項分割任務的通用視覺大腦！** 結合 Qwen3-VL 的語意理解與 SAM2 的精準分割，X2SAM 首次在單一框架內同時支援圖像/影片雙輸入與文字/視覺（點、框）雙提示。其獨創的 **Mask 記憶模組 (Mask Memory Module)** 作為短期視覺工作記憶，在影片推理分割 (V-Rea. Seg.) 上狂飆提升 14.2 個百分點，強勢刷新 SOTA。
  * **解決痛點 / 推薦場景**：**完美解決了過往模型「只能做圖或只能做影片」的架構碎片化痛點，以及影片分割中常見的物體身份跳變與閃爍問題。** 透過 6 幀的 FIFO 記憶機制保持極高的時序一致性。極度適合用於開發**全能型具身智能 (Embodied AI) 連續環境感知系統**、**高互動性影視特效自動摳圖**，以及需要精準追蹤動態目標的**安防監控與自駕車視覺**。
  * **資源**：[🐙 GitHub](https://github.com/wanghao9610/X2SAM) | [📄 論文](https://arxiv.org/abs/2605.00891) | [🌐 專案主頁](https://wanghao9610.github.io/X2SAM)

* **[RNS (Retrieve and Segment)](https://github.com/TilemahosAravanis/Retrieve-and-Segment)** `[CVPR 2026]` 🔥 `[視覺RAG]` `[少樣本分割]` `[測試時適配]`
  * **核心優勢**：**引入「視覺 RAG」的開放詞彙分割破局者，僅需 1 張支援圖即可讓 SAM 2.1 效能暴增 22%！** 徹底拋棄昂貴的離線全局訓練，RNS 是一個檢索增強的「測試時適配器 (Test-time Adapter)」。它在推理時，會針對當前畫面即時檢索最相關的視覺特徵，並與文本特徵動態融合，為每張測試圖「即時」訓練一個專屬輕量分類器，精準彌補了純文本無法捕捉細粒度邊界的缺陷。
  * **解決痛點 / 推薦場景**：**完美解決了傳統開放世界分割中「純文字描述太抽象，但海量像素標註又太昂貴」的兩難痛點。** 企業無需再為冷門類別準備成千上萬的數據，只需提供 1~20 張目標的標註圖（1-shot 到 20-shot），模型就能達到接近全監督的精準度。極度適合用於**工業級罕見瑕疵 AOI 檢測**、**醫療影像特定病灶高精確摳圖**，以及需要快速適配新場景的**客製化自動標註管線**。
  * **資源**：[🐙 GitHub](https://github.com/TilemahosAravanis/Retrieve-and-Segment) | [📄 論文](https://arxiv.org/abs/2602.XXXXX) *(註：以實際 arXiv 連結為準)*

* **[TIPSv2](https://github.com/google-deepmind/tips)** `[CVPR 2026]` 🔥 `[像素級理解]` `[零樣本分割]` `[視覺-語言預訓練]`
  * **核心優勢**：**打破 CLIP 與 DINOv2 局限，達成「像素級」Patch-Text 對齊的視覺編碼器新霸主！** 谷歌開源的 TIPSv2，創新提出 `iBOT++` 掩碼圖像建模目標，首度強制模型「對齊可見 Token 的表徵」，並結合 Head-only EMA 與多粒度文本描述策略。在零樣本分割任務上全面輾壓 SigLIP2 與 DINOv2 (例如 PASCAL VOC 達 62.4 mIoU)，實現前所未有的邊界清晰度與語意一致性。
  * **解決痛點 / 推薦場景**：**完美解決了傳統視覺-語言大模型「認得出貓，但無法精確框出貓的每一寸毛髮（Patch 級別輪廓）」的致命痛點。** 由於大幅提升了特徵圖的平滑度與局部語意捕捉能力，是打造**自動駕駛場景精細感知**、**醫療影像像素級病灶分割**，以及**機器人高精度抓取**等密集預測 (Dense Prediction) 任務的工業級底座首選。
  * **資源**：[🐙 項目頁面與程式碼](https://github.com/google-deepmind/tips)

* **[INSID3](https://visinf.github.io/INSID3)** `[CVPR 2026]` 🔥 `[免訓練分割]` `[DINOv3特化]` `[輕量極速]`
  * **核心優勢**：**打破 SAM 霸權的免訓練 (Training-Free) 分割黑科技，單一凍結 DINOv3 達成 SOTA！** 徹底拋棄傳統 In-Context Segmentation 對額外 Decoder、Fine-tuning 或 SAM 遮罩先驗的重度依賴[cite: 1]。透過首創的「位置去偏 (Positional Debiasing)」與「聚類聚合」機制，讓分割能力直接從 DINOv3 強大的自監督表示中「長出來」[cite: 1]。模型參數僅 304M，單次推論僅需 302 ms，速度與輕量化程度遠超動輒近 1B 參數的 GF-SAM (1,030 ms)[cite: 1]。
  * **解決痛點 / 推薦場景**：**完美解決了傳統視覺模型在更換資料域（如醫療影像）或不同語義粒度時，泛化能力崩潰與硬體資源消耗過大的致命痛點[cite: 1]。** 憑藉卓越的跨圖語義匹配能力，在醫療 X-Ray (+27.8 點)、PASCAL-Part (+6.0 點) 與個人化分割任務上全面輾壓對手[cite: 1]。極度適合資源受限的邊緣設備、高精確度醫療影像分析，以及需要 One-Shot 零樣本提取特定物件的工業級輕量化場景。
  * **資源**：[🐙 項目頁面與程式碼](https://visinf.github.io/INSID3)[cite: 1]

* **[Perceive Anything Model](https://www.alphaxiv.org/zh/overview/2506.05302v1)**：對標 SAM2 + LLM，不僅能分割，還能理解並描述物件。[📝 中文解讀](https://zhuanlan.zhihu.com/p/1919709726209446971)

* **[InstructSAM](https://voyagerxvoyagerx.github.io/InstructSAM/)**
  * **解決痛點**：專為地球觀測打造的免訓練分割框架。輸入指令「標記森林大火區域」，即可自動完成地理圖資分割，災防應變強大輔助。

* **[RemoteSAM](https://deepwiki.com/1e12Leon/RemoteSAM)**：面向地球觀測 (Earth Observation) 的通用分割模型。

* **[MatAnyone](https://github.com/pq-yang/MatAnyone)**：視訊摳圖專用，主打髮絲級還原。

---

## OCR
**📖 OCR (Optical Character Recognition 光學文字識別)**
**[針對物件或場景影像進行分析與偵測](https://www.twman.org/AI/CV)**

- [使用開源模型強化您的 OCR 工作流程](https://huggingface.co/blog/zh/ocr-open-models)
- [12個流行的開源免費OCR項目](https://mp.weixin.qq.com/s/7EuhnQedAX6injBL_Dg_sQ)

隨著大模型技術下放，OCR 已經從單純的「字元辨識」進化為「複雜版面理解 (Document Understanding)」。

👉 *延伸閱讀：[針對物件或場景影像進行分析與偵測 (觀念總結)](https://www.twman.org/AI/CV)* | *[12個流行的開源免費OCR項目](https://mp.weixin.qq.com/s/7EuhnQedAX6injBL_Dg_sQ)*

### 1. 基於視覺大模型 (VLM) 的高精度 OCR
處理手寫字跡、模糊掃描檔與不規則表單的最佳解法。

* **[Chandra OCR 2](https://github.com/datalab-to/chandra)** `[2026-04-16]` 🔥

    * **[Chandra OCR](https://github.com/datalab-to/chandra)** `[2025-10-21]`：標榜超越 DeepSeek-OCR 的革命性突破，支援本地部署。[📝 真實評測](https://zhuanlan.zhihu.com/p/1969019468937144099)
    * **核心優勢**：**擊敗 GPT-4o 與 DeepSeek-OCR 的開源 SOTA 黑馬！** 僅 4B 參數卻具備頂級的「版面感知 (Layout-Aware)」能力。它不僅是提取純文字，而是像人類閱讀一樣理解文檔結構，能精準識別跨頁表格、手寫表單（含核取方塊）與複雜的 LaTeX 數學公式，並直接輸出支援渲染的 Markdown 或 HTML。

    * **解決痛點 / 推薦場景**：**徹底解決傳統 OCR「只認字、不認排版」導致資料破碎的致命痛點。** 原生支援 vLLM 容器化高速批量推論與超過 90 種語言。非常適合用作建構企業 RAG 知識庫的前處理引擎，或是科研論文數位化、歷史手稿與法務合約的自動化解析。

    * **資源**：[🐙 GitHub](https://github.com/datalab-to/chandra) | [🤗 HuggingFace](https://huggingface.co/datalab-to/chandra) | [🌐 官方線上 Playground](https://www.datalab.to/playground)
* **[Qianfan-OCR](https://github.com/baidubce/Qianfan-VL)** `[2026-03-25]` 🔥
  * **核心優勢**：**4B 參數達成「端對端文檔智慧」新標竿，KIE 任務表現超越 Gemini-3.1 Pro。** 百度千帆團隊推出的統一模型，不再需要傳統的偵測與識別分離流程。其核心 **Layout-as-Thought** 機制讓模型在解析文字前先進行佈局推理，大幅提升了對非結構化文檔的理解精度。
  * **解決痛點 / 推薦場景**：**完美解決了傳統 OCR 在處理複雜嵌套表格、多欄排版時「順序錯亂」與「關聯丟失」的問題。** 在 OmniDocBench 等多項權威基準測試中登頂，是目前兼顧「解析精度」與「推論效率」的工業級文檔處理首選。
  * **資源**：[🐙 GitHub](https://github.com/baidubce/Qianfan-VL) | [📄 論文](https://www.google.com/search?q=https://arxiv.org/abs/2603.XXXXX) (待正式釋出) | [📝 官方技術解析](https://www.google.com/search?q=https://cloud.baidu.com/article/qianfan-ocr-unified-model)
* **[DeepSeek-OCR 2](https://github.com/deepseek-ai/DeepSeek-OCR-2/)** `[2026-01-27]` 🔥
  * **核心優勢**：專精複雜場景的高精度文字辨識。能完美應對手寫、模糊與多語系發票，是企業自動化財報系統的高性價比底座。[📝 公眾號解讀](https://mp.weixin.qq.com/s/DOm_hg6DWA_OjcsLuUQ9Hw)
* **[HunyuanOCR](https://github.com/Tencent-Hunyuan/HunyuanOCR)** `[2025-11-30]`：騰訊混元釋出的 1B 級全能模型。
* **[PaddleOCR-VL](https://huggingface.co/PaddlePaddle/PaddleOCR-VL)** `[2025-10-19]`：老牌 OCR 強者推出的視覺大模型版本。
* **[DianJin-OCR-R1](https://github.com/aliyun/qwen-dianjin)** `[2025-08-18]`：點金 OCR，專攻模糊蓋章與跨頁表格。

### 2. PDF 解析與 RAG 資料清洗神器
將複雜排版的文件完美轉換為適合大語言模型閱讀的 Markdown 格式。  

* **[MinerU 2.5-Pro](https://github.com/opendatalab/MinerU)** `[2026-04-16]` 🔥
  * **[MinerU](https://github.com/opendatalab/MinerU)** `[2025-02-05]`：**解決痛點**：將 PDF 完美轉換為乾淨 Markdown 的開源神器。高保真還原數學公式與程式碼區塊，是準備 LLM 訓練語料的必備清洗工具。
  * **核心優勢**：**1.2B 極小參數逆襲 235B 巨獸，RAG 資料清洗的終極殺器！** 上海 AI Lab 重磅升級，憑藉極致的數據工程（四步協同質量飛輪），在 OmniDocBench 評測中擊敗千億級通用大模型。原生支援「跨頁表格自動合併」、「截斷段落接續」與「表格內圖像檢測」。
  * **解決痛點 / 推薦場景**：**徹底解決複雜 PDF (如雙欄論文、密集數學公式、嵌套表格) 轉換 Markdown 時的結構破碎問題。** 不需龐大算力即可精準還原版面邏輯，是企業建置 RAG 私有知識庫、大模型預訓練語料準備絕對不可或缺的高保真清洗神器。
  * **資源**：[🐙 GitHub](https://github.com/opendatalab/MinerU) | [📄 論文](https://arxiv.org/abs/2604.04771) | [📊 評測基準](https://github.com/opendatalab/OmniDocBench)

* **[PDFMathTranslate](https://github.com/PDFMathTranslate/PDFMathTranslate)** `[2025-11-12]` 🔥
  * **核心優勢**：**學術界頂會 EMNLP 2025 認證，地表首款完美保留排版、公式與圖表的 PDF 雙語翻譯大腦！** 採用先進的 `DocLayout-YOLO` 視覺模型進行版面佈局解析，徹底打破傳統 PDF 翻譯工具將公式文字化、導致排版盡毀的黑盒限制。它能精準「解剖」論文結構，完美復刻 LaTeX 數學公式、複雜嵌套表格與文獻引用，並原生對接 OpenAI、DeepL、Google 乃至本地部署的 Ollama 等多元 LLM 推理引擎。全球累積下載量已突破 22 萬次。
  * **解決痛點 / 推薦場景**：**完美解決了科研人員與開發者閱讀 STEM (理工科) 論文時公式錯亂、圖表移位的致命痛點。** 內建五大靈活接入模式（WebUI、CLI 腳本、Docker 隔離部署、MCP 智能體插件以及 Zotero 學術工作流一鍵右鍵翻譯），是企業打造**高保真學術文獻 RAG 知識庫前處理**、**學術團隊極速無障礙文獻調研**的工業級無損知識遷移神作。
  * **資源**：[官方主倉庫 🐙 GitHub](https://github.com/PDFMathTranslate/PDFMathTranslate) | [次世代實驗分支 🐙 GitHub-next](https://github.com/PDFMathTranslate/PDFMathTranslate-next) | [📄 EMNLP 論文](https://aclanthology.org/2025.emnlp-demos.71/) | [📝 arXiv 預印本](https://arxiv.org/abs/2507.03009)


* **[OCRFlux](https://github.com/chatdoc-com/OCRFlux)** `[2025-06-16]`
  * **解決痛點**：專治「反人類排版」的 PDF 解析救星！精準還原雙欄排版與跨頁表格，非常適合建立企業私有知識庫。

* **[markitdown](https://github.com/microsoft/markitdown)** `[2024-12-15]`：微軟官方開源的文件轉換工具。

* **[OmniParser](https://github.com/AlibabaResearch/AdvancedLiterateMachinery/tree/main/OCR/OmniParser)** `[2024-10-29]`：Alibaba 出品，通用文檔複雜場景抽取。

* **[olmocr](https://github.com/allenai/olmocr)** `[2025-03-03]`：支援本地部署精準提取 PDF。

### 3. 輕量化與傳統開源 OCR 生態

* **[Stirling-PDF (全能隱私安全 PDF 處理基礎設施)](https://github.com/Stirling-Tools/Stirling-PDF)** `[持續更新]` 🔥
  * **核心優勢**：**地表最強 100% 本地私有化 PDF 處理神兵利器，橫掃 50+ 種專業編輯與高精度 OCR 功能！** 在 GitHub 狂攬超過 63K Stars，這款基於 Java 的硬核開源專案，讓使用者能透過美觀的網頁介面完全離線操作。它徹底終結了敏感公文或商業機密必須上傳至公有雲轉換的資安洩漏風險，將商業級 PDF 編輯室完美封裝至本地端。
  * **解決痛點 / 推薦場景**：**完美解決了政府機關、金融合規與技術團隊處理機密合約、財務報表時的資料隱私痛點，是終結昂貴商業授權（如 Adobe Acrobat）的終極平替神作。** 原生整合強大的 **OCR 光學字元辨識**，能將沉悶的掃描檔秒變可搜尋、可編輯的乾淨文本。支援大批量 PDF 與 Word、Excel、Markdown、網頁及圖片的雙向無損轉換。極度適合用於**企業內部高度機密檔案處置**、**跨平台自動化財稅發票審計**，以及**大模型 RAG 知識庫前處理的資料去隱私與清洗管線**。
  * **資源**：[🐙 GitHub 官方開源](https://github.com/Stirling-Tools/Stirling-PDF) | [🌐 官方網站](https://www.stirlingpdf.com) | [📦 Docker Hub 鏡像](https://hub.docker.com/r/stirlingpdf/stirling-pdf)

* **[Falcon OCR](https://github.com/tiiuae/falcon-perception)** `[2026-04-01]` 🔥
  * **核心優勢**：**0.3B 極致輕量，效能吊打 10 倍大模型。** 採用與 Falcon Perception 相同的早融合單棧架構專為 OCR 訓練。表格識別準確率達 90.3%，OmniDocBench 總體得分與 DeepSeek OCR v2 等百億參數巨獸不相上下。
  * **解決痛點 / 推薦場景**：**打破高併發文件解析的吞吐量瓶頸。** 在 vLLM 環境下單卡 A100 吞吐量高達驚人的 5825 tok/s。更原生提供 MLX 支援，開發者可直接在 MacBook 上流暢部署，是本地端極速 OCR 的「殺手級」引擎。
  * **資源**：[🐙 GitHub](https://github.com/tiiuae/falcon-perception) | [📄 論文](https://arxiv.org/abs/2603.27365)

* **[OpenDoc-0.1B](https://github.com/Topdu/OpenOCR)** `[2026-01-28]` / **[OpenOCR](https://github.com/Topdu/OpenOCR)** `[2025-03-05]`：極度輕量化的開源 OCR 專案。

* **[dots.ocr](https://huggingface.co/rednote-hilab/dots.ocr)** `[2025-07-30]`：本地部署的 1.7B 超強 OCR。

* **[MonkeyOCR](https://deepwiki.com/Yuliang-Liu/MonkeyOCR)** `[2025-06-05]`：猴子家族的文檔辨識專案。

* **[PP-DocBee](https://github.com/PaddlePaddle/PaddleMIX/tree/develop/deploy/ppdocbee)** `[2025-03-05]`：百度文檔影像理解模型。

* **[GOT-OCR-2.0](https://mp.weixin.qq.com/s/rQL-Q0TGhT6e8Ti4zZalrg)** `[2024-09-11]`：宣告 OCR 2.0 時代來臨的代表作。

* **[RapidOCR](https://github.com/RapidAI/RapidOCR/blob/main/docs/README_zh.md)**：跨平台、高效率的實用 OCR 部署方案。

* **[TableStructureRec](https://github.com/RapidAI/TableStructureRec)**：專門對付複雜表格結構的辨識推理庫。

---

## Diffusion Model
**🎨 Diffusion Model (擴散模型與影像生成)**

擴散模型已經從單純的「文字生圖」，進化到「長影片生成」、「精準控制」與「一體化生成」。以下精選 2025-2026 年最具影響力的開源專案：

### 1. 影片生成大模型 (Video Generation)
突破硬體極限與時長限制，帶來電影級的視覺理解。

* **[Remotion Skills (AI 代碼驅動影片框架)](https://github.com/remotion-dev/skills)** `[持續更新]` 🔥
  * **核心優勢**：**顛覆「黑盒文生影片」，用 AI 寫 React 程式碼來「精確渲染」影片的工程化革命！** 建立在知名的 React 影片框架 Remotion 之上，將影片視為「隨時間變化的 UI」。它內建專為大模型設計的動畫模式庫與 MCP 協議，讓 AI 代理能直接聽懂自然語言指令（如：做一個 30 秒科技風產品介紹），並自動輸出 100% 確定性、可編輯、支援版本控制的 TypeScript/React 影片代碼。
  * **解決痛點 / 推薦場景**：**完美解決了主流生成式 AI 影片無法精確控制排版、無法修改錯字，以及傳統圖形化剪輯軟體無法自動化批量生產的痛點。** 告別手動拖曳時間軸，極度適合企業開發者打造**自動化 RPA 影片生產工廠 (如每日新聞摘要、電商財報可視化)**、**社群媒體短影音批量生成**，是將影片製作從「手工藝」升級為「軟體工程」的開源首選。
  * **資源**：[🐙 Remotion 主專案](https://github.com/remotion-dev/remotion) | [🐙 Remotion Skills (AI技能包)](https://github.com/remotion-dev/skills)
`[程式碼生影片]` `[Agent原生支援]` `[零誤差渲染]` `[自動化剪輯工廠]`

* **[SVOR (Stable Video Object Removal)](https://github.com/xiaomi-research/svor)** `[2026-03]` 🔥 `[影片物件消除]` `[物理感知]` `[高容錯]`
  * **核心優勢**：**CVPR 2026 物理感知視頻實例消除挑戰賽冠軍神作，徹底終結影片消除的「陰影殘留」與「閃爍抖動」！** 由小米大模型應用團隊研發，首創 MUSE (窗口化聯合策略) 與 DA-Seg (去噪感知分割) 模組。透過時間窗口內的多影格聯合分析，即使輸入的 AI 識別遮罩有缺陷，也能穩定追蹤高速動態物件並智能修補邊界。
  * **解決痛點 / 推薦場景**：**完美解決了真實世界影片後製中，物件移除後容易「跟丟導致閃爍」與「殘留反光物理陰影」的致命痛點。** 搭配課程式兩階段訓練（真實背景自監督預訓練＋合成數據精調），極大幅度提升了跨場景的適應力。是打造**高質量影視特效擦除**、**短影音自動去浮水印/路人**，以及推動**智慧影片編輯工具商用落地**的工業級開源首選。
  * **資源**：[🐙 GitHub](https://github.com/xiaomi-research/svor) | [📄 論文](https://arxiv.org/abs/2603.09283) | [⚡ Skill 快速調用](https://clawhub.ai/wangfei1204/mi-visionforge-svor) | [🏆 挑戰賽榜單](https://docs.google.com/spreadsheets/d/18qfBQesVNpHadUP_cdL6T8hPGH_cXrnJ94Z5H-zuibs)

* **[Wan-Video (萬相)](https://github.com/Wan-Video/Wan2.1)** `[2025-02-25]`
  * **核心優勢**：阿里萬相大模型開源，主打全模態、全尺寸的高解析度影片生成。[📝 媒體報導](https://finance.sina.com.cn/jjxw/2025-02-26/doc-inemukxr9127437.shtml)

* **[SkyReels V2](https://github.com/SkyworkAI/SkyReels-V2)** `[2025-04-22]`：全球首個無限時長影片生成模型，具備電影級的場景理解能力。

* **[MAGI-1](https://github.com/SandAI-org/Magi-1)** `[2025-04-22]`：Sand AI 推出的全球首個自回歸影片生成大模型。

* **[Phantom](https://github.com/Phantom-video/Phantom)** `[2025-04-24]`：字節跳動開源。極度友善的硬體門檻，僅需 10G 顯存即可生成 1280x720 高清影片。

* **[Index-AniSora](https://deepwiki.com/bilibili/Index-anisora)** `[2025-05-19]`：B 站開源的 SOTA 動畫影片生成模型，二次元風格特化。

* **[MAI-Image-2](https://microsoft.ai/news/today-were-announcing-3-new-world-class-mai-models-available-in-foundry/)** `[2026-04-16]` 🔥
  * **核心優勢**：**重新定義「廣告級」影像生成，畫面內文字清晰度與光影質感超越 DALL-E 3。** Microsoft AI 專為設計師打造，精準捕捉自然膚色紋理與細膩光影。其最強大的亮點在於解決了生成式 AI 常見的「圖中文字扭曲」痛點，能直接產出可商用的排版設計。
  * **解決痛點 / 推薦場景**：**解決了設計師在生成海報或 UI 時，必須手動修正文字與光影不自然的繁瑣流程。** 榮登 Arena.ai 榜單前三，是電商廣告創作、專業平面設計與社交媒體視覺素材的工業級利器。
  * **資源**：[🌐 Microsoft MAI Playground](https://www.google.com/search?q=https://microsoft.ai/playground) | [📄 官方發布報告](https://microsoft.ai/news/today-were-announcing-3-new-world-class-mai-models-available-in-foundry/)

### 2. 極速生成與大一統架構 (Speed & Unified Models)

* **[Vision Banana](https://vision-banana.github.io/)** `[2026-04]` 🔥
  * **核心優勢**：**迎來視覺領域的 LLM 時刻！以「圖像生成」一統 2D/3D 感知任務的通用視覺霸主。** Google DeepMind 重磅發布（何愷明與謝賽寧聯合支持），基於 Nano Banana Pro 圖像生成基座打造。它徹底打破「一任務一模型」的孤島，首創將語義分割、實例分割與 3D 深度/表面法線估計，全部轉化為「生成可解碼 RGB 圖像」的單一任務。在零樣本 (Zero-shot) 設定下，其分割效能強勢超越專用模型 SAM 3，深度估計更在「無相機內參」的嚴苛條件下擊敗 Depth Anything V3。
  * **解決痛點 / 推薦場景**：**完美解決了傳統視覺任務需要海量特定標註資料、模型架構臃腫，以及 3D 任務極度依賴硬體相機參數的致命痛點。** 透過極簡的「自然語言指令微調」，同一套權重即可無縫切換多種感知能力，且完全不犧牲原有的高畫質文生圖與圖像編輯性能。這是引領 AI 走向「視覺大語言模型」時代的燈塔級專案，極度適合用於構建**通用具身智能 (Embodied AI) 視覺大腦**、**零樣本自動駕駛環境感知**與**全能型多模態 Agent**。
  * **資源**：[🌐 專案主頁](https://vision-banana.github.io/) | [📄 官方論文 (arXiv:2604.20329)](https://arxiv.org/abs/2604.20329) | [📝 謝賽寧深度點評](https://x.com/sainingxie/status/2047339789926429166)
  <br>`[生成即理解]` `[零樣本 SOTA]` `[超越 SAM 3]` `[通用視覺基座]`

* **[Nucleus-Image 17B](https://github.com/WithNucleusAI/Nucleus-Image)** `[2026-04]` 🔥
  * **核心優勢**：**全球首個將 MoE (混合專家) 架構引入文生圖領域的擴散大模型**。具備高達 170 億參數的龐大知識容量，但每次推論（Inference）僅需激活約 20 億參數。獨創「解耦路由機制」與「文本 KV 緩存加速」，不需依賴 RLHF 偏好微調，純預訓練效能即超越 Imagen 4，並在空間位置理解上輾壓 FLUX.1。
  * **解決痛點 / 推薦場景**：完美解決了傳統頂尖生圖模型「吃顯存、推理極慢、算力成本高昂」的致命痛點，真正實現「大模型品質，小模型成本」。對於需要高併發、低延遲生成複雜畫面（例如：精準物件排版、高難度密集提示詞遵循）的企業級 AI 繪圖服務與商業設計平台，這是極具性價比的新一代開源基座首選。
  * **資源**：[🐙 GitHub](https://github.com/WithNucleusAI/Nucleus-Image) | [🤖 ModelScope](https://modelscope.cn/models/NucleusAI/Nucleus-Image)
    <br>`[MoE擴散模型]` `[極低推理成本]` `[精準空間佈局]`

* **[Sana (ICLR 2025 Oral)](https://github.com/NVlabs/Sana)** `[2025-01-28]` 🔥
  * **核心優勢**：由 NVIDIA、MIT 與清華共同開源。導入新架構，生成高清圖片的速度比 FLUX 快 100 倍！[📝 中文解讀](https://zhuanlan.zhihu.com/p/19489214543)

* **[Jodi](https://vipl-genun.github.io/Project-Jodi/)** `[2025-05-28]`：視覺理解與生成大一統模型，打破辨識與生成的界線。

* **[FlashVideo](https://github.com/FoundationVision/FlashVideo)** `[2025-02-14]`：字節跳動視訊增強演算法，102 秒即可生成 1080P 影片。

### 3. ComfyUI 實用工具與精準控制
專注於解決 AI 生成過程中的臉部崩壞、手部變形與硬體限制。

* **[RefineAnything](https://github.com/limuloo/RefineAnything)** `[2026-04]` 🔥 `[局部精修]` `[背景凍結]` `[Qwen-Image底座]`
  * **核心優勢**：**完美終結 AI 生圖「修臉壞背景、改字大走鐘」的局部修復黑科技！** 基於 Qwen2.5-VL 多模態架構，首創反直覺的「Focus-and-Refine (裁剪-放大-修復-無縫貼回)」策略。它將高解析度運算資源 100% 集中在瑕疵區域，搭配專屬的邊界一致性損失函數，實現了背景結構相似性 (SSIMbg) 高達 0.9997 的驚人表現（背景近乎紋絲不動）。
  * **解決痛點 / 推薦場景**：**徹底解決了傳統擴散模型 (Diffusion Models) 進行局部重繪 (Inpainting) 時，容易導致「換臉」失真、手部越修越畸形、文字 Logo 無法還原，甚至意外竄改非編輯區背景的致命痛點。** 這是打造**電商產品細節無痕替換**、**廣告海報文字與 Logo 修正**，以及**人物崩壞特徵救援工作流**的工業級首選。
  * **資源**：[🐙 GitHub](https://github.com/limuloo/RefineAnything) | [📄 論文](https://arxiv.org/abs/2604.06870) | [🌐 專案主頁](https://limuloo.github.io/RefineAnything)

* **[FramePack](https://github.com/kijai/ComfyUI-FramePackWrapper)** `[2025-04-14]`：ComfyUI 擴充神套件，能在 6G 顯存下跑 13B 模型，最高支援生成 1 分鐘的長影片。

* **Flux 生態系與控制網**：
  * **[Flux Models 官方底座](https://huggingface.co/black-forest-labs)**：目前最強開源生圖底座。
  * **[PuLID](https://github.com/ToTheBeginning/PuLID)** `[2024-11-29]`：極強的人物特徵保持與換臉工具。
  * **[Leffa](https://github.com/franciszzj/Leffa)** `[2024-12-17]`：Meta AI 推出的人物特徵保持方案。

* **[HivisionIDPhotos](https://deepwiki.com/Zeyi-Lin/HivisionIDPhotos)** `[2025-05-23]`：超實用！智慧證件照生成神器，全自動精準摳圖、換背景、裁切任意尺寸。

* **[ComfyUI Impact Pack](https://github.com/ltdrdata/ComfyUI-Impact-Pack)**：ComfyUI 必裝節點包，提供最強臉部與細節修復。

* **[AnomalyAny (CVPR 2025)](https://hansunhayden.github.io/AnomalyAny.github.io/)** `[2025-05-27]`：利用 Stable Diffusion 協助進行視覺異常檢測，完全無需訓練。

---

## Digital Human
**🧑‍💻 Digital Human (虛擬數字人)**

虛擬數字人技術結合了語音驅動 (Audio-Driven)、唇形對齊 (Lip-Sync) 與 3D 渲染，是目前 AI 客服與虛擬直播的技術核心。

### 1. 語音驅動與動態頭像生成 (Audio-Driven Avatar)

* **[CyberVerse](https://github.com/dsd2077/CyberVerse)** `[2026-04-18]` 🔥 `[即時視訊對話]` `[零建模單圖生成]` `[WebRTC流式傳輸]` `[全鏈路Agent]`
  * **核心優勢**：**真正意義上的 JARVIS 級開源即時數位人神作，單張照片即可開啟超低延遲視訊對話！** 採用極致的微服務與熱插拔插件架構，內建 WebRTC P2P 與 LiveKit SFU 雙流模式。徹底打破傳統數位人「預錄、回合制」的侷限，無縫整合 FlashHead/LiveAct 視覺驅動、Qwen Omni 語音大模型、RAG 記憶資料庫與 Agent 工具調用，實現「視覺、聽覺、執行」三位一體的全鏈路即時互動。
  * **解決痛點 / 推薦場景**：**完美解決了以往開源數位人「對話延遲高達數秒」、「不支援語音即時打斷 (Voice Barge-in)」以及「缺乏後台任務執行力」的致命痛點。** 結合 GPU 分散式推理與首次預熱機制，成功將首幀延遲壓縮至 1.5 秒以內。是企業低成本打造**24 小時高擬真視訊客服**、**沉浸式 AI 陪伴角色**，以及**跨硬體裝置具身智能中樞**的工業級首選框架。
  * **資源**：[🐙 GitHub 官方開源](https://github.com/dsd2077/CyberVerse) | [📄 官方中文技術文件](https://github.com/dsd2077/CyberVerse/blob/main/README.zh-CN.md)

* **[LongCat-Video-Avatar 1.5](https://github.com/meituan-longcat/LongCat-Video)** `[2026-05]` 🔥
  * **核心優勢**：**打破數字人「完美演練」的實驗室假象，真正走向商用落地的極速影片生成霸主！** 由美團團隊開源，搭載 Whisper-large 音訊解碼器，並首創將 GRPO 偏好對齊細化至逐幀層面，完美修正了手部畸變與長時序動作崩塌。最震撼的是引入 DMD (Distribution Matching Distillation) 蒸餾技術，將 50 步生成暴力壓縮至 8 步，達成 15 倍推理加速（10 秒影片僅需 1 分鐘），徹底引爆規模化商用潛能。
  `[8步極速生成]` `[GRPO偏好對齊]` `[多人互動支援]` `[商業級擬真]`
  * **解決痛點 / 推薦場景**：**完美解決了傳統虛擬人「講長句口型崩壞」、「多人同框時嘴部亂動」以及「生成太慢吃垮算力」的致命痛點。** 憑藉極高的身份一致性與音畫協調度，在盲測中強勢擊敗 Kling Avatar 2.0 與 HeyGen。是打造**高併發電商直播帶貨**、**千人千面的 AI 客服/講師**，以及**複雜多人互動情境**的工業級基礎模型首選。
  * **資源**：[🐙 GitHub](https://github.com/meituan-longcat/LongCat-Video) | [📄 官方技術報告](https://github.com/meituan-longcat/LongCat-Video/blob/main/assets/LongCat-Video-Avatar-1.5-Tech-Report.pdf) | [🌐 專案主頁與線上 Demo](https://meigen-ai.github.io/LongCat-Video-Avatar-1.5-Page/)

* **[InfiniteTalk](https://github.com/Meituan-AutoML/InfiniteTalk)** `[2026-04]` 🔥
  * **核心優勢**：**打破「面癱」配音魔咒，首創「全身聯動」的無限時長說話影片生成模型！** 由美團 (MeiGen-AI) 團隊重磅開源 (Apache 2.0)。採用獨創的「稀疏幀影片配音」範式與流式音訊驅動架構，支援圖生影片 (I2V) 與影片到影片 (V2V)。它全面超越 MuseTalk 等傳統僅能「修補嘴型」的方案，不僅對口型，更能讓數字人的頭部動作、面部表情與身體姿態完美契合音訊節奏。
  * **解決痛點 / 推薦場景**：**徹底解決傳統 AI 虛擬人「身體僵硬、表情死板」以及生成長度受限的致命痛點。** 具備強大的軟參考機制，能在極致保留原始人物身份與背景的同時，實現無卡頓的幀間平滑過渡。生態系極度友善，已原生支援 ComfyUI 節點與低顯存量化加速。極度適合教育工作者零門檻打造**生動的虛擬講師微課**，也是**影視多語言在地化無縫配音**與**高互動遊戲 NPC 動畫**的工業級首選。
  * **資源**：[🐙 GitHub (Meituan-AutoML)](https://github.com/Meituan-AutoML/InfiniteTalk) | [📄 技術報告](https://arxiv.org/abs/2504.09459) | [🌐 專案主頁與線上 Demo](https://meituan-automl.github.io/InfiniteTalk/)
  <br>`[全身同步]` `[無限時長]` `[開源可商用]` `[ComfyUI支援]`

* **[StreamAvatar](https://streamavatar.github.io)** `[2025-12]` 🔥
  * **核心優勢**：**打破高質量、實時性與強交互的「不可能三角」，首創具備「聆聽反應」的流式擴散數字人！** 由清華、人大與騰訊混元聯合發表。透過創新的自回歸蒸餾（Auto-regressive Distillation），將傳統笨重的雙向 DiT 模型轉化為僅需 3 步去噪的因果生成器。在雙 H800 GPU 環境下，達成 1.20 秒超低延遲與 RTF < 1 的完美實時串流生成。
  * **解決痛點 / 推薦場景**：**徹底解決傳統擴散模型「無法即時串流」、「長時生成身份漂移」以及「只會說不會聽」的三大致命傷。** 獨創 Reference Sink 機制確保長影片不變形，並導入音訊交互注意力模組，讓數字人在用戶說話時能給出點頭、微笑等極度自然的「聽覺反饋」。是打造次世代雙向視訊客服、高保真 AI 實況主與沉浸式虛擬陪伴的巔峰架構。
  * **資源**：[🌐 官方專案主頁與 Demo](https://streamavatar.github.io) | [📄 論文](https://arxiv.org/abs/2512.22065)

* **[SoulX-LiveAct](https://github.com/Soul-AILab/SoulX-LiveAct)** `[2026-03-16]` 🔥
  * **核心優勢**：**首款突破「小時級」穩定生成的實時數字人框架，低延遲且具備極致性價比。** 來自 Soul App AI Lab，首創 Neighbor Forcing 與 ConvKV Memory 技術，解決了 AR 擴散模型在流式生成中常見的身份漂移與顯存爆量問題。在 H100 達成 20 FPS、0.94s 延遲，甚至支援在 RTX 5090 等消費級顯卡上流暢運行。
  * **解決痛點 / 推薦場景**：**徹底解決長時直播中常見的「人物變形」與「顯存線性增長」瓶頸。** 提供高精準度的口型同步 (Sync-C: 9.40) 與動作/表情 JSON 精細控制。是打造 24 小時不斷線直播、實時視訊通話（FaceTime 級體驗）與企業級虛擬客服的技術天花板方案。
  * **資源**：[🐙 GitHub](https://github.com/Soul-AILab/SoulX-LiveAct)

* **[Live Avatar](https://github.com/Alibaba-Quark/LiveAvatar)** `[持續更新]` 🔥
  * **核心優勢**：**阿里巴巴 (Quark) 開源的 14B 頂規即時交互數字人模型。** 建立在強大的 `Wan2.2-S2V-14B` 基礎模型之上，支援流式生成（Streaming Generation），能透過單張照片與音訊，生成畫質極高且「無限時長」的動態說話影片。
  * **解決痛點 / 實戰避坑指南**：**主打「再也不用真人直播」，但硬體要求極為嚴苛。** 完美解決了 24 小時虛擬直播帶貨的需求，但**部署前請注意**：這是一頭在電腦裡跑的大象，強烈建議使用具備 **24GB 顯存** 的顯卡（如 RTX 3090/4090）進行推理。12GB 顯卡極易觸發 CUDA Out of Memory (OOM) 報錯。適合擁有高階算力、追求極致畫質與無斷點直播的企業級用戶。
  * **資源**：[🐙 GitHub](https://github.com/Alibaba-Quark/LiveAvatar) | [🌐 官方專案主頁](https://liveavatar.github.io/)

* **[SoulX-FlashTalk](https://github.com/Soul-AILab/SoulX-FlashTalk)** `[2025-12-24]` 🔥
  * **核心優勢**：**14B 參數數字人開源新標竿，0.87 秒極速啟動 + 32 FPS 實時流生成。** Soul AI Lab 針對實時交互場景打造的重磅模型，首創「雙向流蒸餾技術」與「多步回顧自校正機制」。不僅將訓練效率暴力提升 23 倍，更打破了傳統模型長序列生成的崩壞魔咒，實現亞秒級的超低延遲與高保真吞吐。
  * **解決痛點 / 推薦場景**：**徹底終結數字人長時直播「越播越崩」與「身份漂移」的致命痛點。** 具備強大的長時生成穩定性，完美支援 7×24 小時不斷線實時互動。極度適合用於高強度的電商 AI 直播帶貨、需要極低延遲的視訊智能客服，以及元宇宙多語言虛擬社交場景。
  * **資源**：[🐙 GitHub](https://github.com/Soul-AILab/SoulX-FlashTalk) | [📄 論文](https://arxiv.org/abs/2512.23379) | [🌐 官方 Demo 與展示](https://soul-ailab.github.io/soulx-flashtalk/) | [🤗 HuggingFace 權重](https://huggingface.co/Soul-AILab/SoulX-FlashTalk-14B)

* **[JoyStreamer-Flash](https://joystreamer.github.io/)** `[2025-12]`
  * **核心優勢**：強大的音訊驅動 (Audio-driven) 自回歸擴散模型。具備即時推論能力，且標榜支援「無限時長 (Infinite-length)」的數字人與影片生成，是打造長時間不斷線 AI 實況主的極佳底座。

* **[EchoMimic V3](https://github.com/antgroup/echomimic_v3)** `[持續更新]` 🔥
  * **核心優勢**：**螞蟻集團開源的統一多模態人體動畫生成大模型。** V3 版本底層大換血，深度整合了 `Wan2.1-Fun-V1.1-1.3B` 與 `wav2vec2-base-960h`，進一步強化了臉部表情的細節與唇形同步的精準度，是目前最受矚目的開源數字人框架之一。
  * **解決痛點 / 實戰避坑指南**：**高畫質但硬體門檻極高，部署前請注意算力評估。** 雖然官方曾聲稱 12GB 顯存可運行，但根據開發者最新實測，在生成高幀數影片時，單一 Python 進程顯存極易飆破 21GB（甚至在 RTX 4090 D 上遭遇 OOM）。**部署建議**：需嚴格檢查模型權重路徑（如 `models/transformer`），並適度在 `app_mm.py` 中下調 `num_frames`（分段長度）以降低顯存壓力。適合具備高階算力（如 24G+ VRAM）的企業級開發者進行二次開發。
  * **資源**：[🐙 GitHub](https://github.com/antgroup/echomimic_v3) | [🤗 Wan2.1 基礎模型](https://huggingface.co/alibaba-pai/Wan2.1-Fun-V1.1-1.3B-InP) | [🤖 魔搭 ModelScope 權重](https://modelscope.cn/models/BadToBest/EchoMimicV3) | [📝 V3 官方原理解讀](https://mp.weixin.qq.com/s/cHL-ROirvxLxJNtabke0Fg)

* **[Fantasy-talking](https://fantasy-amap.github.io/fantasy-talking/)** `[2025-04-14]`：基於強大的 Wan2.1 影片生成底座，打造的高畫質音訊驅動數字人。

* **[Hallo3 (CVPR 2025)](https://github.com/fudan-generative-vision/hallo3)**：復旦大學開源，主打高度動態且極具表現力的肖像動畫生成。

* **[FlowAct-R1](https://grisoon.github.io/FlowAct-R1/)**：基於流匹配技術的高效能數字人生成框架。

### 2. 完整互動系統與 3D 建模 (Interactive System & 3D)

* **[OpenTalking](https://github.com/datascale-ai/opentalking)** `[2026-05]` 🔥
  * **核心優勢**：**打通從 Demo 到生產部署的最後一哩路，工業級「全鏈路」實時數字人編排框架！** 它不重複造底層模型的輪子，而是專注於產線編排，將 LLM 流式對話、句級 TTS、口型同步渲染與 WebRTC 低延遲傳輸完美串接。首創「樂高式」可插拔設計，無縫相容輕量級 Wav2Lip 到高質量 FlashTalk，更原生支援華為昇騰 910B 等企業級 NPU 私有化部署。
  `[工業級編排]` `[實時互動]` `[WebRTC低延遲]` `[全鏈路串接]`
  * **解決痛點 / 推薦場景**：**完美解決了傳統數字人開源專案「只能做短片 Demo」、「缺乏實時打斷控制」與「模組碎片化難以整合」的致命痛點。** 透過 100-300ms 的極低 WebRTC 傳輸延遲與精細的事件流控制，提供從「5 分鐘免顯卡 API 快速體驗」到「本地端高畫質渲染」的四階段落地路徑。是企業打造**高併發電商虛擬直播帶貨**、**24 小時無斷點視訊客服**、以及**高沉浸感 AI 陪伴角色**的底層中樞首選。
  * **資源**：[🐙 GitHub 官方開源](https://github.com/datascale-ai/opentalking) | [🌐 官方架構解析](https://github.com/datascale-ai/opentalking/blob/main/docs/architecture.md) | [📦 OmniRT 模型服務庫](https://github.com/datascale-ai/omnirt)

* **[PersonaLive](https://github.com/GVCLab/PersonaLive)** `[CVPR 2026]` 🔥
  * **核心優勢**：**打破硬體高牆的無限時長虛擬主播，12GB 顯存即刻開播！** 澳門大學與大灣區大學 GVC Lab 研發的即時肖像動畫框架。首創流式生成策略（Streaming Generation），將影片分塊處理，徹底解決傳統擴散模型生成長影片時「顯存隨時間線性暴增」導致 OOM 的致命瓶頸。單張靜態照片即可透過攝像頭即時驅動，支援 TensorRT 加速與 WebUI 互動。
  `[流式生成]` `[無限時長]` `[低硬體門檻]` `[ComfyUI支援]`
  * **解決痛點 / 推薦場景**：**完美解決了傳統數位人系統需要昂貴動捕設備或頂規顯卡才能長時段直播的痛點。** 極度適合缺乏高階算力的個人創作者與中小企業，用於打造**高擬真虛擬實況主 (VTuber)**、**線上教育虛擬講師**與**隱私保護視訊會議**。專案生態成熟，已原生支援 ComfyUI 工作流與 Apache-2.0 商業授權。
  * **資源**：[🐙 GitHub 官方開源](https://github.com/GVCLab/PersonaLive) | [📄 arXiv 論文](https://arxiv.org/abs/2512.11253) | [📦 ComfyUI 擴展節點](https://github.com/okdalto/ComfyUI-PersonaLive)

* **[Linly-Talker](https://github.com/Kedreamix/Linly-Talker)** `[持續更新]` 🔥
  * **核心優勢**：**開源數字人界的「多模態全家桶」，高度模組化的智能交互系統！** 在 GitHub 狂攬 3.1K+ Stars，它打破了單純「圖片轉影片」的框架，將 ASR (Whisper)、LLM 大腦 (Qwen/Gemini)、TTS 音色克隆 (GPT-SoVITS) 與面部驅動 (SadTalker/MuseTalk) 完美串接。支援流式語音與 WebRTC 即時通訊，模組可按需求自由抽換。
  * **解決痛點 / 推薦場景**：**徹底推翻了高質量數字人需要昂貴動捕設備與專業團隊的成本高牆。** 只需要「一張任意人像照片 + 一段語音/文字」，就能打造具備上下文記憶、會聽、會說、會動的專屬 AI 分身。極度適合低成本部署虛擬面試官、24 小時 AI 客服、線上教育導師，或是支援本地端部署的隱私安全對話機器人。
  * **資源**：[🐙 GitHub](https://github.com/Kedreamix/Linly-Talker)

* **[Open Avatar Chat](https://zread.ai/HumanAIGC-Engineering/OpenAvatarChat)**：爆火的開源神器，主打本地部署、無套路，輕鬆打造個人虛擬助理。

* **[MimicTalk (NeurIPS 2024)](https://github.com/yerfor/MimicTalk)**：專注於 3D Talking Face 生成的學術級框架。

* **商用級別開源 (克隆與真人還原)**：
  * **[Duix](https://github.com/GuijiAI/duix.ai)**：全球首個開源的「真人」數字人系統。
  * **[HeyGem](https://github.com/GuijiAI/HeyGem.ai)**：被譽為數字人克隆神器，高度還原真人神態。

---

## 🖼️ Image Recognition (基礎圖像識別)

在追求酷炫的生成式 AI 之前，理解圖像分類的底層架構仍然是電腦視覺的必修課。以下是從 CNN 時代走向 Transformer 時代的三大奠基之作：

* **[EUPE (Efficient Universal Perception Encoder)](https://arxiv.org/pdf/2603.22387)** `[2026-03]` 🔥 `[通用視覺編碼器]` `[多任務聚合]` `[邊緣運算]`
  * **核心優勢**：**終結視覺基礎模型「嚴重偏科」的開源神作，單一輕量編碼器完美聚合 CLIP、DINO 與 SAM 的多領域超能力！** Meta Reality Labs 創新提出「先擴展再縮小」的兩階段蒸餾範式（先由巨型代理教師融合跨域知識，再固定解析度蒸餾給輕量學生模型），徹底突破了過往高效編碼器無法兼顧「全局語意理解」與「像素級密集預測」的瓶頸，各項基準測試效能全面輾壓 NVIDIA 的 RADIO 系列。
  * **解決痛點 / 推薦場景**：**完美解決了傳統電腦視覺專案為了應付不同任務，必須「同時掛載多個專家模型」導致記憶體爆滿、硬體算力消耗過大的致命痛點。** EUPE 的極致高效與統一的特徵空間，不僅是資源極度受限的**邊緣運算設備 (Edge AI)** 與**多任務工業視覺感知系統**的落地首選，更是為下一代**多模態大語言模型 (MLLM)** 裝上了一雙能同時看懂語意與幾何細節的「全能之眼」。
  * **資源**：[📄 arXiv 論文](https://arxiv.org/pdf/2603.22387)

* **[ViT (Vision Transformer)](https://github.com/google-research/vision_transformer)**
  * **技術意義**：Google 團隊將 NLP 領域的 Transformer 架構完美移植到視覺領域的開山之作，徹底改變了 CV 的發展軌跡。[📝 解析文章](https://zhuanlan.zhihu.com/p/445122996)

* **[Swin Transformer](https://github.com/microsoft/Swin-Transformer)**
  * **技術意義**：微軟開源。透過移動窗口 (Shifted Window) 機制，解決了 ViT 運算量過大與難以處理多尺度物件的問題，「用 CNN 的方式打敗了 CNN」。[📝 原理通俗解析](https://zhuanlan.zhihu.com/p/362690149)

* **[EfficientNetV2](https://github.com/d-li14/efficientnetv2.pytorch)**
  * **技術意義**：CNN 架構的極致優化版。透過神經架構搜尋 (NAS)，在極小的參數規模下達到了前所未有的準確度與訓練速度。[📝 更小更快的訓練解析](https://zhuanlan.zhihu.com/p/361873583)

---

## Document AI
**📄 Document AI (文檔理解與複雜排版解析)**

傳統 OCR 只能單純提取文字，但真實世界的文檔（如財報、發票、學術論文）充滿了複雜的表格與版面設計。本區塊收錄了從「版面分析」到「端對端解析」的核心基礎模型：

### 1. 端對端與無 OCR 解析框架 (End-to-End & OCR-Free)
跳過傳統的文字檢測與辨識步驟，直接將圖片轉化為結構化文本。

* **[Infinity-Parser2](https://github.com/infly-ai/INF-MLLM)** `[2026-05]` 🔥
  * **核心優勢**：**打破大廠閉源壟斷的文檔解析天花板，單一模型通吃六大任務的開源霸主！** 徹底拋棄傳統 OCR 繁瑣的「版面分析 + 表格辨識 + 文字提取」多階段 Pipeline。透過首創的「可驗證獎勵聯合強化學習」，一個端到端模型就能完美解析複雜雙欄排版、跨頁表格、甚至高難度的 LaTeX 數學公式與化學式。在權威 ParseBench 中，其 35B Pro 版得分 (74.3%) 強勢超越 Gemini-3-Pro，而 2B Flash 版更能以 1624 tokens/s 的極速狂飆。
  * **解決痛點 / 推薦場景**：**完美解決企業建置 RAG (檢索增強生成) 系統時「PDF 轉 Markdown 格式破碎、表格資料流失」的致命痛點。** 告別難以維護的舊式 OCR 工具鏈。Flash 版 (2B) 非常適合部署於算力受限的邊緣運算設備或高併發的 C 端應用；Pro 版 (35B) 則是打造**企業級私有知識庫**、**科研論文自動化歸檔**與**醫療/金融報表深度解析**的工業級清洗神器。
  * **資源**：[🐙 GitHub 官方源碼](https://github.com/infly-ai/INF-MLLM) | [🤗 HuggingFace 線上體驗](https://huggingface.co/spaces/infly/Infinity-Parser2-Demo)
  `[RAG前處理]` `[端到端解析]` `[超越Gemini]` `[極速推論]`

* **[Logics-Parsing (含 Omni/v2)](https://github.com/alibaba/Logics-Parsing)** `[2026-03]` 🔥
  * **核心優勢**：阿里開源的端對端 (End-to-End) 文件解析王者。採用單一模型架構，完全拋棄了傳統複雜的多階段 Pipeline。
  * **解決痛點**：能直接將圖片轉換為帶有邏輯標籤的「結構化乾淨 HTML」。不僅能看懂高難度的排版，連複雜的數理公式、甚至化學結構式都能智慧識別並精準轉成 SMILES 格式，是目前建立企業 RAG 知識庫的最強清洗方案。
* **Donut (2022)**：OCR-free Document Understanding Transformer。不依賴底層 OCR 引擎的文檔理解架構。[📄 arXiv:2111.15664](./donut.md)
* **Nougat (2023)**：Neural Optical Understanding for Academic Documents。Meta 推出的學術文獻解析神器，能完美處理論文中的數學公式與排版。[📄 arXiv:2308.13418](https://facebookresearch.github.io/nougat/)

### 2. 版面分析與視覺預訓練模型 (Layout Analysis & Pre-training)
* **LayoutParser (2021)**：基於深度學習的文檔版面分析統一工具包，提供強大的開箱即用 API。[📄 arXiv:2103.15348](./LayoutParser.md)
* **DiT (2022)**：Document Image Transformer。專為文檔影像設計的自監督預訓練模型，大幅提升下游任務效能。[📄 arXiv:2203.02378](./DiT.md)
* **TrOCR (2021)**：微軟提出的 Transformer-based OCR 模型，首創結合預訓練影像與語言模型的文字識別架構。[📄 arXiv:2109.10282](./TrOCR.md)

<details>
<summary><strong>📚 經典 LayoutLM 家族系列 (點擊展開)</strong></summary>
由微軟亞研院 (MSRA) 提出，開啟了圖文多模態文檔理解的新紀元。
<ul>
  <li><b>LayoutLM (2020)</b>: 首次將文字與版面位置 (Layout) 聯合預訓練。[📄 arXiv:1912.13318](./LayoutLM.md)</li>
  <li><b>LayoutLMv2 (2021)</b>: 引入視覺特徵的多模態預訓練升級版。[📄 arXiv:2012.14740](./LayoutLMv2.md)</li>
  <li><b>LayoutXLM (2021)</b>: 支援多語系的視覺化文檔理解大模型。[📄 arXiv:2104.08836](./LayoutXLM.md)</li>
  <li><b>LayoutLMv3 (2022)</b>: 統一文本與影像 Masking 機制的預訓練架構。[📄 arXiv:2204.08387](./LayoutLMv3.md)</li>
</ul>
</details>

### 3. 場景文字辨識 (Scene Text Recognition)
專門對付自然場景中形狀扭曲、光影複雜的文字辨識。
* **ABINet (2021)**：主打「像人類一樣閱讀」，結合語言模型進行視覺特徵的迭代糾錯。[📄 arXiv:2103.06495](./ABINet.md)
* **ABINet++ (2022)**：ABINet 的進化版，強化了文字定位與語言建模的交互深度。[📄 arXiv:2211.10578](./ABINet%2B%2B.md)
* **ABCNet v2 (2021)**：自適應貝茲曲線網路 (Adaptive Bezier-Curve Network)，專治任意形狀的彎曲文字與招牌。[📄 arXiv:2105.03620](./ABCNet_v2.md)
* **SVTR (2022)**：單一視覺模型的場景文字識別，捨棄了複雜的 RNN 架構，在推論速度與準確率上取得雙優。[📄 arXiv:2205.00159](./SVTR.md)

---

## DeepFake Detection
**🕵️‍♂️ DeepFake Detection (深度偽造與換臉偵測)**

隨著生成式 AI (AIGC) 的爆發，如何防範惡意的 AI 換臉與造假成為資安重頭戲。以下收錄 CVPR 2021 針對深度偽造偵測的三大經典防禦架構：

* **Multi-attentional Deepfake Detection**
  * **核心概念**：多重注意力機制。透過捕捉臉部不同區域（如五官邊緣、紋理）的微小竄改痕跡來提升偵測準確率。*(H. Zhao et al., CVPR 2021)*
* **Geometric Features**
  * **核心概念**：精確幾何特徵提取。分析臉部器官的幾何比例與邊緣連續性，藉此提升對抗各種偽造技術的穩健性 (Robustness)。*(Sun, Zekun et al., CVPR 2021)*
* **3D Decomposition**
  * **核心概念**：3D 臉部解構。將 2D 影像逆向分解為 3D 形狀、光照與紋理特徵，從物理立體空間的合理性中，找出換臉演算法的破綻。*(Xiangyu Zhu et al., CVPR 2021)*

<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "TechArticle",
  "mainEntityOfPage": {
    "@type": "WebPage",
    "@id": "https://deep-learning-101.github.io/Computer-Vision"
  },
  "headline": "2026 電腦視覺 (Computer Vision) 工業級模型資源彙整",
  "description": "一份詳盡的電腦視覺（Computer Vision）資源清單，內容涵蓋異常檢測(AOI)、物件偵測、圖像分割、高精度OCR、擴散模型與影片生成，協助企業與開發者快速導入開源視覺技術。",
  "image": "https://raw.githubusercontent.com/Deep-Learning-101/TonTon/refs/heads/main/_includes/DL101-Logo.jpg",
  "author": {
    "@type": "Organization",
    "name": "Deep Learning 101, Taiwan",
    "url": "https://deep-learning-101.github.io/"
  },
  "publisher": {
    "@type": "Organization",
    "name": "Deep Learning 101, Taiwan",
    "logo": {
      "@type": "ImageObject",
      "url": "https://raw.githubusercontent.com/Deep-Learning-101/TonTon/refs/heads/main/_includes/DL101-Logo.jpg"
    }
  },
  "datePublished": "2026-03-29",
  "dateModified": "2026-03-29",
  "keywords": "電腦視覺, Computer Vision, YOLO, 目標偵測, OCR, 異常檢測, AOI, 圖像分割, SAM2, 擴散模型, 影片生成, 數位人, 發票解析, 機器視覺",
  "about": {
    "@type": "Service",
    "serviceType": "AI Consulting",
    "provider": {
      "@type": "Organization",
      "name": "Deep Learning 101, Taiwan"
    },
    "name": "人工智慧顧問服務 (AI Consulting)",
    "description": "提供關於電腦視覺（Computer Vision）領域的專業顧問服務，包含演算法開發、模型選擇、應用落地與技術導入。"
  }
}
</script>