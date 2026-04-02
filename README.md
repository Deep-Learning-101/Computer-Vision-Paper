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

* **[LLM2CLIP](https://microsoft.github.io/LLM2CLIP/)** `[2026-01-29]` 🔥
  * **核心優勢**：微軟開源黑科技！結合大語言模型 (LLM) 強大的常識推理能力來增強 CLIP 模型的視覺表徵。
  * **解決痛點**：完美解決了傳統 CLIP 在遇到罕見工業瑕疵或長尾分佈數據時容易誤判的問題，非常適合用於高精度的零樣本瑕疵檢測。[📄 AlphaXiv 論文](https://www.alphaxiv.org/abs/2411.04997) | [📝 公眾號深度解讀](https://mp.weixin.qq.com/s/-U03e1KZmFCoXTGzdYbC0Q)
* **[AA-CLIP](https://deepwiki.com/Mwxinnn/AA-CLIP)** `[2025-04-12]`：透過 Anomaly-Aware 機制增強 CLIP 的零樣本異常檢測能力。
* **[AnomalyCLIP](https://deepwiki.com/zqhang/AnomalyCLIP)** `[2025-04-27]`：Object-agnostic Prompt Learning，實現跨物體的零樣本異常偵測。
* **[AdaptCLIP](https://github.com/aiiu-lab/AdaptCLIP)** `[2025-05-15]`：將 CLIP 模型適配為通用的視覺異常檢測器。
* **[Multi-Modal LLM for AD (VELM)](https://deepwiki.com/Sassanmtr/VELM)** `[2025-05-05]`：不僅偵測異常，還能進行分類與動作建議的工業多模態架構。

### 2. 少樣本與無監督學習前沿突破 (Few-shot & Unsupervised)
解決現場只能取得「正常良品圖」或極少量瑕疵圖的痛點。

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
* **[Meta SAM 3](https://github.com/facebookresearch/sam3)**
  * **核心優勢**：Meta 官方最新分割一切模型，持續推進零樣本分割的極限。[📝 公眾號解讀](https://mp.weixin.qq.com/s/7uDHXQd1ES2mV4dZFB7VMw)
  
* **Meta SAM 2 及其變體**：
  * [**Meta SAM 2 官方**](https://ai.meta.com/sam2/) | [📝 60行程式碼微調教學](https://mp.weixin.qq.com/s/YfgYCzvi0cXxOFIfQvE_9w)
  * [**SAM2Long**](https://github.com/Mark12Ding/SAM2Long)：解決 SAM 2 長影片追蹤容易丟失目標的問題，影視特效自動摳圖利器。
  * [**SAM2Point**](https://github.com/ZiyuGuo99/SAM2Point)：將 SAM 2 的能力延伸至 3D 點雲數據，為自駕車光達 (LiDAR) 與 3D 醫學影像帶來零樣本分割能力。
  * [**Grounded SAM 2**](https://github.com/IDEA-Research/Grounded-SAM-2)：結合文字 grounding 技術，在影片中追蹤特定物件。

### 2. 領域特化與多模態分割模型
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

* **[DeepSeek-OCR 2](https://github.com/deepseek-ai/DeepSeek-OCR-2/)** `[2026-01-27]` 🔥
  * **核心優勢**：專精複雜場景的高精度文字辨識。能完美應對手寫、模糊與多語系發票，是企業自動化財報系統的高性價比底座。[📝 公眾號解讀](https://mp.weixin.qq.com/s/DOm_hg6DWA_OjcsLuUQ9Hw)
* **[Chandra OCR](https://github.com/datalab-to/chandra)** `[2025-10-21]`：標榜超越 DeepSeek-OCR 的革命性突破，支援本地部署。[📝 真實評測](https://zhuanlan.zhihu.com/p/1969019468937144099)
* **[HunyuanOCR](https://github.com/Tencent-Hunyuan/HunyuanOCR)** `[2025-11-30]`：騰訊混元釋出的 1B 級全能模型。
* **[PaddleOCR-VL](https://huggingface.co/PaddlePaddle/PaddleOCR-VL)** `[2025-10-19]`：老牌 OCR 強者推出的視覺大模型版本。
* **[DianJin-OCR-R1](https://github.com/aliyun/qwen-dianjin)** `[2025-08-18]`：點金 OCR，專攻模糊蓋章與跨頁表格。

### 2. PDF 解析與 RAG 資料清洗神器
將複雜排版的文件完美轉換為適合大語言模型閱讀的 Markdown 格式。


* **[MinerU](https://github.com/opendatalab/MinerU)** `[2025-02-05]`
  * **解決痛點**：將 PDF 完美轉換為乾淨 Markdown 的開源神器。高保真還原數學公式與程式碼區塊，是準備 LLM 訓練語料的必備清洗工具。
* **[OCRFlux](https://github.com/chatdoc-com/OCRFlux)** `[2025-06-16]`
  * **解決痛點**：專治「反人類排版」的 PDF 解析救星！精準還原雙欄排版與跨頁表格，非常適合建立企業私有知識庫。
* **[markitdown](https://github.com/microsoft/markitdown)** `[2024-12-15]`：微軟官方開源的文件轉換工具。
* **[OmniParser](https://github.com/AlibabaResearch/AdvancedLiterateMachinery/tree/main/OCR/OmniParser)** `[2024-10-29]`：Alibaba 出品，通用文檔複雜場景抽取。
* **[olmocr](https://github.com/allenai/olmocr)** `[2025-03-03]`：支援本地部署精準提取 PDF。

### 3. 輕量化與傳統開源 OCR 生態
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

* **[Wan-Video (萬相)](https://github.com/Wan-Video/Wan2.1)** `[2025-02-25]`
  * **核心優勢**：阿里萬相大模型開源，主打全模態、全尺寸的高解析度影片生成。[📝 媒體報導](https://finance.sina.com.cn/jjxw/2025-02-26/doc-inemukxr9127437.shtml)
* **[SkyReels V2](https://github.com/SkyworkAI/SkyReels-V2)** `[2025-04-22]`：全球首個無限時長影片生成模型，具備電影級的場景理解能力。
* **[MAGI-1](https://github.com/SandAI-org/Magi-1)** `[2025-04-22]`：Sand AI 推出的全球首個自回歸影片生成大模型。
* **[Phantom](https://github.com/Phantom-video/Phantom)** `[2025-04-24]`：字節跳動開源。極度友善的硬體門檻，僅需 10G 顯存即可生成 1280x720 高清影片。
* **[Index-AniSora](https://deepwiki.com/bilibili/Index-anisora)** `[2025-05-19]`：B 站開源的 SOTA 動畫影片生成模型，二次元風格特化。

### 2. 極速生成與大一統架構 (Speed & Unified Models)
* **[Sana (ICLR 2025 Oral)](https://github.com/NVlabs/Sana)** `[2025-01-28]` 🔥
  * **核心優勢**：由 NVIDIA、MIT 與清華共同開源。導入新架構，生成高清圖片的速度比 FLUX 快 100 倍！[📝 中文解讀](https://zhuanlan.zhihu.com/p/19489214543)
* **[Jodi](https://vipl-genun.github.io/Project-Jodi/)** `[2025-05-28]`：視覺理解與生成大一統模型，打破辨識與生成的界線。
* **[FlashVideo](https://github.com/FoundationVision/FlashVideo)** `[2025-02-14]`：字節跳動視訊增強演算法，102 秒即可生成 1080P 影片。

### 3. ComfyUI 實用工具與精準控制
專注於解決 AI 生成過程中的臉部崩壞、手部變形與硬體限制。


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
* **[SoulX-LiveAct](https://github.com/Soul-AILab/SoulX-LiveAct)** `[2026-03]` 🔥
  * **核心優勢**：Soul AI Lab 推出的黑科技，主打「小時級 (Hour-Scale)」即時人類動畫生成。能在極低的硬體成本下，以 20 FPS 的速度進行即時串流推論，非常適合虛擬直播場景。
* **[JoyStreamer-Flash](https://joystreamer.github.io/)** `[2025-12]`
  * **核心優勢**：強大的音訊驅動 (Audio-driven) 自回歸擴散模型。具備即時推論能力，且標榜支援「無限時長 (Infinite-length)」的數字人與影片生成，是打造長時間不斷線 AI 實況主的極佳底座。
* **[EchoMimic V3](https://github.com/antgroup/echomimic_v3)** / **[EchoMimic V2 (CVPR 2025)](https://github.com/antgroup/echomimic_v2)**
  * **核心優勢**：螞蟻集團開源的強大框架。V3 版本進一步強化了臉部表情的細節與唇形同步的精準度，是目前最穩定的開源選項之一。[📝 V3 公眾號解讀](https://mp.weixin.qq.com/s/cHL-ROirvxLxJNtabke0Fg)
* **[Fantasy-talking](https://fantasy-amap.github.io/fantasy-talking/)** `[2025-04-14]`：基於強大的 Wan2.1 影片生成底座，打造的高畫質音訊驅動數字人。
* **[Hallo3 (CVPR 2025)](https://github.com/fudan-generative-vision/hallo3)**：復旦大學開源，主打高度動態且極具表現力的肖像動畫生成。
* **[FlowAct-R1](https://grisoon.github.io/FlowAct-R1/)**：基於流匹配技術的高效能數字人生成框架。

### 2. 完整互動系統與 3D 建模 (Interactive System & 3D)
* **[Linly-Talker](https://github.com/Kedreamix/Linly-Talker)**：不只是生影片！這是一個結合 LLM 與視覺模型的「智能交互系統」，可以直接用來打造虛擬面試官或 AI 客服。
* **[Open Avatar Chat](https://zread.ai/HumanAIGC-Engineering/OpenAvatarChat)**：爆火的開源神器，主打本地部署、無套路，輕鬆打造個人虛擬助理。
* **[MimicTalk (NeurIPS 2024)](https://github.com/yerfor/MimicTalk)**：專注於 3D Talking Face 生成的學術級框架。
* **商用級別開源 (克隆與真人還原)**：
  * **[Duix](https://github.com/GuijiAI/duix.ai)**：全球首個開源的「真人」數字人系統。
  * **[HeyGem](https://github.com/GuijiAI/HeyGem.ai)**：被譽為數字人克隆神器，高度還原真人神態。

---

## 🖼️ Image Recognition (基礎圖像識別)

在追求酷炫的生成式 AI 之前，理解圖像分類的底層架構仍然是電腦視覺的必修課。以下是從 CNN 時代走向 Transformer 時代的三大奠基之作：

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