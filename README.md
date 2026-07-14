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

> **核心摘要：**
> 2026年電腦視覺聚焦於多模態融合與少樣本學習。本指南精選 YOLOv11、擴散模型及高精度 OCR 等逾40項開源技術，助企業提升產線良率至99%，降低標註成本達80%，實現端對端工業級視覺檢測。

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

* **[CCL (Contextual Consistency Learning)](https://openaccess.thecvf.com/content/CVPR2026/papers/Li_Consistency_Beyond_Contrast_Enhancing_Open-Vocabulary_Object_Detection_Robustness_via_Contextual_CVPR_2026_paper.pdf)** `[2026-03-29]` 🔥 `[開放詞彙檢測]` `[訓練側增強]` `[零推理延遲]` `[跨場景泛化]`
  * **核心優勢**：**打破「換個工位、光源或治具模型就飄移」的產線易碎惡夢，首創訓練側「造背景 + 壓特徵」的跨場景不變性增強範式！** 這項由哈工大深圳、鵬城實驗室與香港中文大學團隊發表於 CVPR 2026 的硬核成果，直擊開放詞彙目標檢測 (OVOD) 在工業落地時，模型極易將背景紋理與環境噪聲錯誤綁定到目標本體的致命盲區。CCL 另闢蹊徑，完全不改動上線模型結構與推理延遲：先透過「背景生成模組 (CBDG)」利用 SAM 分割前景並結合大模型與 Stable Diffusion 批量量產「同缺陷、不同治具/光照背景」的擾動樣本對；再藉由「上下文一致性損失 (CCLoss)」在視覺與文本雙重維度強制約束模型特徵，大幅將開放世界檢測指標 (OmniLabel) 強勢拉升 16.3% AP。
  * **解決痛點 / 推薦場景**：**完美解決了 PCB 質檢、金屬表面外觀、電池片及倉儲揀選等高度柔性產線中，因「批次切換、夾具變更、相機角度微調導致 Domain Shift，使線下漂亮指標一上線就崩潰」的剛需痛點。** 由於其具備「推理零負擔」與「隨插即用」的插件式可遷移特質（實測在 GLIP 與 FIBER 底座上抗背景干擾能力直接翻倍），企業能以極低成本無痛升級現有檢測器。是打造**高泛化跨工位智慧質檢系統**、**拒絕頻繁補數據重訓的工業級數據閉環管線**的次世代防翻車首選方案。
  * **資源**：[📄 論文 (CVF 原文)](https://openaccess.thecvf.com/content/CVPR2026/papers/Li_Consistency_Beyond_Contrast_Enhancing_Open-Vocabulary_Object_Detection_Robustness_via_Contextual_CVPR_2026_paper.pdf) | [📝 跨場景泛化技術解讀](https://mp.weixin.qq.com/s/tvA28GTA8kzEOSkLsFvQoA)

* **[ViT³ (ViT with Test-Time Training)](https://github.com/LeapLabTHU/ViTTT)** `[2025-12-16]` 🔥 `[視覺長序列建模]` `[線性複雜度]` `[極限省顯存]` `[CVPR 2026 Best Paper Finalist]`
  * **核心優勢**：**打破 Vision Transformer 的 $O(N^2)$ 算力死結，首創「梯度下降非線性壓縮」將推論速度暴力拉升 4.6 倍、顯存狂降 90.3% 的次世代視覺骨幹神作！** 這項由清華大學與阿里巴巴團隊聯手打造、入圍 CVPR 2026 最高榮譽（入圍率 < 0.1%）的史詩級工作，徹底顛覆了傳統 Linear Attention 易漏細節與 Mamba 隱狀態容量有限的 Failure Mode。ViT³ 引入「臨場學習 (Test-Time Training)」範式，將當前輸入的 K/V Token 視為迷你數據集，在推論當下對內部微型網路（首選 3×3 深度卷積 DWConv）進行單輪全批次自監督訓練，用非線性自適應權重完美鎖住「全域上下文 + 局部感受野」，成功在 $O(N)$ 線性複雜度下解鎖 Transformer 的極致表達力。
  * **解決痛點 / 推薦場景**：**完美解決了超高畫質影像、長影片分析、多模態長上下文及高解析度擴散模型（DiT）在邊緣設備或高併發場景下「Token 數量一拉高，顯存直接原地爆炸」的硬體高牆。** 論文推出非層級（ViT³）、四階段層級通用骨幹（H-ViT³）與擴存生成（DiT³）三大變體。實測在 1248×1248 超高畫質場景下（高達 6084 個 Token），其壓榨硬體的省流表現極具統治力。極度適合用於**4K/8K 超高畫質影音智慧安防監控**、**大尺寸醫學影像病灶微小特徵追蹤**，以及追求**極致性價比的端側 AI 部署與離線視覺檢索管線**。
  * **資源**：[🐙 GitHub 官方開源](https://github.com/LeapLabTHU/ViTTT) | [📄 論文 (arXiv:2512.01643)](https://arxiv.org/pdf/2512.01643) | [📝 慢思考與 TTT 拓撲深度解讀](https://geonuk-kimmm.github.io/UniSpector) *(註：相關技術解讀同步收錄於前沿開集社群)*

* **[ViCrop-Det](https://arxiv.org/abs/2604.26806)** `[2026-04-29]` 🔥
  * **核心優勢**：**打破小目標檢測的算力魔咒，首創「免訓練、即插即用」的空間注意力熵 (SAE) 智能裁剪框架。** 這款由華中科技大學提出的神作，巧妙利用 DETR 檢測器內建的交叉注意力分布作為「內生探針」，透過計算香農熵精準揪出模型「不確定且重要」的區域（即小目標藏身處）進行局部高解析度重檢測。僅需微幅增加約 20% 計算量，即可在 VisDrone 數據集上穩定提升近 3 個百分點的 mAP，以極高的推理幀率 (38.6 FPS) 徹底碾壓 SAHI 等暴力全圖切片方法。
  * **解決痛點 / 推薦場景**：**完美解決了 Transformer 檢測器在密集場景中「注意力被空曠背景稀釋導致微小目標蒸發」，以及傳統 SAHI 切片法「計算量線性暴增」的致命痛點。** 由於無需重新訓練且不更動網路架構，極度適合企業直接掛載於現有模型上，部署於**無人機航拍 (UAV) 密集微小物件偵測**、**自駕車遠距離行人辨識**，以及**衛星遙感影像大圖分析**等計算資源受限但需極高精度的邊緣運算場景。<br>`[免訓練即插即用]` `[小目標檢測]` `[碾壓SAHI]` `[邊緣運算首選]`
  * **資源**：[🐙 GitHub (待釋出搜尋)](https://github.com/search?q=ViCrop-Det+Hui+Wang+HUST) | [📄 論文](https://arxiv.org/abs/2604.26806) | [📝 深度解讀](https://mp.weixin.qq.com/s/UQZENPtcQ-M2AiQu41OKcg)

* **[FS-DETR](https://github.com/YT3DVision/FSDETR)** `[2026-04-21]` 🔥 `[小目標偵測]` `[頻域空間融合]` `[邊緣運算]`
  * **核心優勢**：**打破極端小目標漏檢魔咒，首創「頻域-空間」雙軌融合的輕量級檢測神作！** 基於 RT-DETR 架構進行深度魔改，創新引入二維快速傅立葉變換 (FFT2D) 提取高頻紋理，並結合空間層次注意力 (SHAB) 與可變形稀疏採樣 (DA-AIFI)。在參數僅有 14.7M（比 RT-DETR-R18 瘦身 26%）的極致輕量化條件下，仍能精準捕捉僅數十像素的微小物體，小目標檢測效能 (APₛ) 強勢輾壓 D-Fine-M 與 RT-DETRv2。
  * **解決痛點 / 推薦場景**：**完美解決了傳統 YOLO/DETR 在邊緣設備上「縮小模型就嚴重漏檢、做大模型又跑不動」，以及全局注意力容易被密集背景雜訊干擾的致命痛點。** 實測在 VisDrone (高密度交通) 與 TinyPerson (極端低對比度微小行人) 等嚴苛資料集上創下 SOTA。是打造**無人機高空巡檢 (UAV)**、**衛星遙感影像分析**，以及部署於算力極限**邊緣運算盒子 (Edge AI)** 的工業級首選。
  * **資源**：[🐙 GitHub 官方開源](https://github.com/YT3DVision/FSDETR)

* **[FT-FSOD (跨域小樣本目標偵測框架)](https://arxiv.org/abs/2603.28182)** `[2026-03]` 🔥
  * **核心優勢**：**CVPR 2026 頂會神作！首創「混合集成解碼器 (HED)」打破解碼層串行瓶頸，無需昂貴的生成式數據擴增，即可榨出底座模型的跨域極限！** 透過將 Transformer 解碼層從「純串聯」改為「分層＋並行分支」形成強大的隱式集成，並結合自動感知學習停滯期的「漸進式微調 (Progressive Fine-tuning)」策略，在 RF100-VL 跨域百大數據集榜單上大幅碾壓 SAM3。
  * **解決痛點 / 推薦場景**：**完美解決了企業在導入「冷門/邊緣場景（如：稀有工業缺陷檢測、特規醫學影像、水下探測）」時，面臨「真實標註極缺、預訓練大模型水土不服且微調極易崩潰過擬合」的致命痛點。** 無需為不同資料集痛苦手調超參數，模型在面對完全陌生的 OOD (分佈外) 雜訊樣本時展現極高克制力與穩定性，是資料受限下打造高可靠度跨域 AOI 質檢系統的工業級首選。
  * **資源**：[🐙 GitHub](https://github.com/Intellindust-AI-Lab/FT-FSOD) | [📄 論文](https://arxiv.org/abs/2603.28182)
  <br>`[小樣本偵測]` `[跨域泛化]` `[隱式集成解碼]` `[免數據擴增]`

**B. 亞洲/中國頂尖開源 (極致效能與端側特化)**

| 模型名稱 | 開發團隊 | 💡 核心優勢與突破點 | 🚀 推薦場景 & 規格標籤 |
| :--- | :--- | :--- | :--- |
| **YOLOv10** | 🇨🇳 **清華大學** | **徹底消滅 NMS**。首次在 YOLO 家族中移除後處理的非極大值抑制 (NMS)，大幅降低推理延遲。 | 即時自動駕駛、無人機視覺<br>`[無後處理]` `[超低延遲]` |
| **VisionReasoner** | 🇨🇳 **開源社群** | **統一視覺感知與推理**。利用強化學習技術，標榜效能可對標 Qwen2.5-VL 等大型視覺模型。 | 複雜場景理解、視覺問答<br>`[強化學習]` `[大模型對標]` |
| **MCL** | 🇨🇳 **AAAI 2025** | **遙感影像專家**。專為空拍、衛星圖設計的半監督目標檢測框架 (Multi-clue Consistency Learning)。 | 農業監測、空拍圖分析<br>`[遙感特化]` `[半監督學習]` |

* **[HR-SemNet (High-Resolution Network for Small Object Detection)](https://doi.org/10.1109/TIP.2026.3654770)** `[2026-03]` 🔥 `[小目標神作]` `[無人機巡檢]` `[計算量腰斬]` `[極致輕量]`
  * **核心優勢**：**徹底顛覆傳統 YOLO 瘋狂加深網路的老路，首創「高解析度主幹 + 局部上下文語義補丁」，用 5% 的參數量實現超越大模型的越級打怪！** 發表於頂級期刊 IEEE TIP 2026 的里程碑神作。該模型一針見血地指出微小目標在深層下採樣容易被抹平、且深層全局語義過強會引發背景噪訊的「相對過擬合」痛點。HR-SemNet 另闢蹊徑，主幹網路大膽瘦身，僅保留 P1/P2 兩級超高解析度特徵以鎖定幾何邊界，並在內部瓶頸層逐步嵌入輕量化 LCSM 模組。實測在不破壞小目標空間細節的條件下，比 YOLOv8-P2 基準直接暴漲 3.0 點 AP，而運算量 (GFLOPs) 狂砍 49.9%，模型參數量更是不可思議地縮減了 94.9%（僅剩 5.9M）！
  * **解決痛點 / 推薦場景**：**完美解決了無人機高空巡檢 (UAV)、衛星遙感影像分析、高密度交通監控等嚴苛場景下「微小目標在低解析度層形體消失」以及「背景噪訊導致誤檢飆高」的工業級致命痛點。** 由於徹底消滅了深層網路的冗餘計算，該架構極度適合部署於算力受限的邊緣運算盒子 (Edge AI)、嵌入式設備或穿戴式智慧硬體，是目前處理極密集、低對比度、僅數十像素微小物體的次世代輕量化首選。
  * **資源**：[📄 官方論文 (IEEE TIP)](https://doi.org/10.1109/TIP.2026.3654770) | [📊 dblp 條目](https://dblp.org/rec/journals/tip/PengCLCYX26) | [📝 中文技術解讀](https://mp.weixin.qq.com/s/AW6z4V29PrKSTCSh99RGRg)

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

> **無監督異常檢測是突破 AOI 產線良率瓶頸的關鍵。** 導入 PatchCore 等特徵對齊架構，僅需 50 張正常樣本即可將瑕疵檢出率提升至 98% 以上。此方法有效解決工業製造中缺陷樣本稀缺的問題，降低 60% 漏檢風險。傳統 AOI (自動光學檢測) 高度依賴大量瑕疵樣本來訓練模型。但在真實工業場景中，收集數千張「特定種類」的瑕疵圖往往不切實際。近年來，異常檢測技術已轉向**少樣本 (Few-shot)** 與 **零樣本 (Zero-shot)** 學習。以下為 2025-2026 年最具代表性的開源方案：

* **[Rethinking Transfer Learning for Industrial Inspection: DINOv3 vs. ImageNet Pretraining Across RGB and X-ray Tasks](https://arxiv.org/abs/2605.23472)** `[2026-05]` 🔥 `[工業選型指南]` `[遷移學習重新審視]` `[反直覺硬核實測]`
  * **核心優勢**：**一針見血戳破視覺基礎模型「全能萬用」的神話，為產線 AOI 演算法選型提供最清醒的硬體算力與天花板帳本！** 這篇發表於 CVPR 2026 (Findings) 的里程碑論文，不談學術站隊，直接將當前最強自監督基礎模型 DINOv3 與傳統 ImageNet 監督預訓練丟進真實工業任務（Severstal 鋼板劃傷、Rubber Rings 橡膠缺陷、GDXray 鑄件氣孔等）進行硬碰硬實測。研究給出兩大反直覺技術定性：第一，在可見光 (RGB) 表面缺陷上，DINOv3 紅利極度依賴「全參數微調」，「凍結 Backbone 躺贏」完全是偽命題；第二，在 X-ray 等非可見光強模態偏移任務中，DINOv3 明顯翻車，傳統 ImageNet 預訓練反而從頭到尾展現驚人的穩健度。
  * **解決痛點 / 推薦場景**：**完美解決了自動光學檢測 (AOI) 團隊在專案早期「盲目追新押錯預訓練路線，導致後期天價標註人力、產線節奏與 GPU 算力全面返工」的骨灰級痛點。** 這是資安架構師與演算法工程師在決定模型底座時的「避坑指南」：如果你的專案是**可見光表面瑕疵檢測且算力允許放開骨幹全微調**，果斷選 DINOv3 以換取超高收斂上限；如果是**焊縫透照、安檢、無損探傷 (NDT) 等工業透視場景**，請堅守 ImageNet 監督預訓練，那才是工程上最保險、最不易翻車的解法。
  * **資源**：[📄 官方論文 (arXiv:2605.23472)](https://arxiv.org/abs/2605.23472) | [📝 實驗復盤與遷移學習資料包](https://mp.weixin.qq.com/s/pbPTSgD97i-DfK_hu0SNBQ) *(註：參考資料來源與導讀對應)*

* **[Omni-AD: A Large-scale and Versatile Benchmark for Industrial Anomaly Detection](https://omni-ad.github.io)** `[2026-06-25]` 🔥 `[工業異常通用基準]` `[真實產線數據]` `[雙協議評測]` `[大模型質檢噩夢]`
  * **核心優勢**：**徹底打破 IAD 領域效能飽和僵局，首創相容傳統無監督與多模態大模型 (MLLM) 雙協議的 3.5 萬張真實產線巨量基準！** 由浙江大學、海康機器人、西交大與中大（深圳）發表的 CVPR 2026 燈塔級工作。數據庫直接覆蓋 16 個工業賽道、150 個真實流水線產品類別（規模達 MVTec 的 10 倍）。最破壞性的創新在於它填補了 MLLM 在工業質檢上的評測空白，定義了「缺陷判別、細粒度分類、視覺定位 (Visual Grounding)」三級遞進任務，並經人工與 U-Net 雙重循環像素級精細標註，成為檢驗 AI 演算法是否具備真實產線落地能力的硬核試金石。
  * **解決痛點 / 推薦場景**：**完美解決了傳統工業異常檢測（IAD）基準在實驗室指標動輒破 99% 飽和、導致選型失效，以及多模態大模型在開放世界泛化強、一進產線「精準定位」卻集體崩潰的致命盲區。** 橫向評測揭露了殘酷的現實：最強的 Qwen3-VL-Thinking (30B) 在零樣本定位任務上的 F1 分數僅 26.20%（人類專家為 79.32%），而經典 PatchCore 的 AUPRO 也在這直接跌破 82%。這套大規模通用基準極度適合**企業進行大模型質檢方案與檢索演算法的選型初篩**、**中大型智慧製造廠建構跨品類少樣本預訓練模型底座**，是演算法團隊跨越「線下指標漂亮，上線誤檢漏檢不斷」工程鴻溝的剛需利器。
  * **資源**：[📄 論文 (CVF Open Access)](https://openaccess.thecvf.com/content/CVPR2026/papers/Shi_Omni-AD_A_Large-scale_and_Versatile_Benchmark_for_Industrial_Anomaly_Detection_CVPR_2026_paper.pdf) | [🌐 專案主頁](https://omni-ad.github.io)

### 1. 結合 LLM 與多模態的零樣本檢測 (Zero-shot AD)
利用大語言模型或 CLIP 龐大的常識庫，在「沒看過瑕疵樣本」的情況下，直接透過文字描述或視覺特徵揪出異常。

* **[Fine-VAD (Fine-Grained Video Anomaly Detection)](https://teacher.bupt.edu.cn/zhuangzirui/zh_CN/index.htm)** `[2026-06]` 🔥 `[細粒度異常檢測]` `[影片安防]` `[CLIP多級對齊]` `[漸進式學習]`
  * **核心優勢**：**打破傳統 VAD「只能抓錯、無法指認」的極限，首創「漸進式跨粒度學習」的影片理解神作！** 這篇 CVPR 2026 來自北京郵電大學的重磅論文，徹底拋棄了「一上來就逼模型硬背細分類」的低效煉丹法。透過凍結的 CLIP 圖像編碼器搭配時序適配器 (Temporal Adapter)，它巧妙引導模型經歷「粗粒度 (正常/異常) → 中粒度 (K-Means 宏類別) → 細粒度 (具體異常)」的三層語意洗禮。這套降維打擊策略在 UCF-Crime 權威基準上將 mAP 狂暴拉升近 47.7%，且依然保持 43.25 FPS 的即時推論速度！
  * **解決痛點 / 推薦場景**：**完美解決了智慧城市與園區監控中「光知道有異常還不夠，必須精確分辨是縱火、鬥毆還是車禍才能派單應變」的實戰痛點，並強勢克服了異常行為類內變異大、類間極易混淆的死穴。** 這套不依賴海量細粒度標註的學習範式，極度適合用來打造**城市級智慧安防監控系統 (City Security)**、**工廠/工地高危險工安行為預警**，以及**長影片弱監督理解的自動化 AI 巡檢大腦**。
  * **資源**：[📄 官方論文 (CVPR 2026)](https://openaccess.thecvf.com/content/CVPR2026/papers/Zhang_Fine-VAD_Towards_Fine-Grained_Video_Anomaly_Detection_via_Progressive_Cross-Granularity_Learning_CVPR_2026_paper.pdf) | [🌐 作者實驗室主頁 (追蹤開源動態)](https://teacher.bupt.edu.cn/zhuangzirui/zh_CN/index.htm)

* **[WinCLIP (Zero-/Few-Shot Anomaly Classification and Segmentation)](https://github.com/caoyunkang/WinClip)** `[2023-06]` 🔥 `[零樣本AOI]` `[CLIP特徵升維]` `[狀態提示詞]` `[冷啟動救星]`
  * **核心優勢**：**打破工業 AOI 瑕疵檢測「冷啟動無缺陷樣本」的死局，首創基於 CLIP 的零/少樣本異常分割框架！** 這篇 CVPR 2023 的開創性神作，巧妙解決了通用 CLIP 模型「只見全局物體、不見局部微小瑕疵」的缺陷。透過引入「多尺度窗口化 (Windowing)」提取特徵，並結合涵蓋破損、污染等描述的「狀態提示詞 (State Prompts)」，WinCLIP 能在完全不看過任何缺陷樣本的條件下，精準定位異常區域。其進階版 WinCLIP+ 僅需 1~4 張「正常良品」照片作為參照記憶，AUROC 即可強勢突破 95%。
  * **解決痛點 / 推薦場景**：**完美解決了新產品剛投產時「缺陷樣本極度稀缺、無法訓練專用模型」的致命痛點。** 徹底改變過去「先收壞樣本才能上線」的傳統思維，讓模型能力變成開箱即用的配置。極度推薦給面臨**少量多樣 (High-Mix Low-Volume) 生產線的 AOI 團隊**，是工廠新料號冷啟動、初期異常預先篩檢，以及建構「跨品類通用質檢平台」的最佳起手式。
  * **資源**：[📄 官方論文 (CVPR 2023)](https://openaccess.thecvf.com/content/CVPR2023/papers/Jeong_WinCLIP_Zero-Few-Shot_Anomaly_Classification_and_Segmentation_CVPR_2023_paper.pdf) | [🐙 GitHub (非官方開源復現)](https://github.com/caoyunkang/WinClip)

* **[CoPS (Conditional Prompt Synthesis for Zero-Shot Anomaly Detection)](https://arxiv.org/abs/2508.03447)** `[2026-07]` 🔥 `[零樣本跨域]` `[條件化動態提示]` `[工業醫學雙全能]` `[SAGA空間感知]`
  * **核心優勢**：**徹底打破 CLIP 靜態提示詞無法泛化未知缺陷的魔咒，首創「看圖說話、現場合成提示詞」的自適應工業異判神作！** 這項由中科大、清華與華中科大等頂尖團隊發表的 CVPR 2026 最新前沿成果，直擊傳統 AdaCLIP 和 AnomalyCLIP 提示詞「寫死」、無法應對產線多樣化真實特徵的痛點。CoPS 透過「顯式狀態 Token 合成 (ESTS)」提取精準的正常/異常局部視覺原型，並利用 VAE 隱式採樣融合跨類別語義 Token，將冰冷的文字模板升級為可隨輸入影像動態調整的「條件化提示詞」。在工業與醫學 8 大主流資料集上（包含 MVTec-AD、VisA 與 BrainMRI）橫掃全場，創下平均分類 AUROC 92.5%、分割 AUROC 94.1% 的歷史新高紀錄。
  * **解決痛點 / 推薦場景**：**完美解決了工業與醫學「冷啟動」場景下，因未知缺陷、長尾分佈形態、強大跨類別域偏移，導致傳統多模態模型「看得懂概念，卻框不準局部極小瑕疵」的致命盲區。** 透過其空間感知全局–局部對齊機制 (SAGA)，能將粗粒度的原型匹配完美過渡到細粒度像素級定位，可清晰抓出螺絲微小劃痕或大腦 MRI 病灶。極度適合用於**高度多樣少量（High-Mix Low-Volume）的工件表面瑕疵柔性初篩**、**高精確度醫療影像（HeadCT / BrainMRI）全自動病灶快速篩查**，以及缺乏大量缺陷樣本的**次世代多模態視覺 Agent 質檢管線**。
  * **資源**：[📄 論文](https://arxiv.org/abs/2508.03447) | [📝 深度技術解讀](https://mp.weixin.qq.com/s/pbPTSgD97i-DfK_hu0SNBQ)

* **[GS-CLIP (Geometry-Aware Prompt and Synergistic View Representation Learning)](https://github.com/zhushengxinyue/GS-CLIP)** `[2026-03-29]` 🔥
  * **核心優勢**：**首創「文本幾何翻譯 + 視覺雙流並行」兩階段框架，打破 2D 投影的有損壓縮盲區，全面制霸零樣本 3D 異常檢測！** 這篇由蘇州大學與清華大學 AIR 團隊聯手發表的 CVPR 2026 重量級神作，徹底解決了現有方法將 3D 點雲壓平至 2D 時，關鍵立體幾何細節大量丟失的致命缺陷。GS-CLIP 在文本端透過「幾何缺陷蒸餾模組 (GDDM)」動態將 3D 局部與全域形狀特徵翻譯為提示詞，讓 CLIP 預先理解幾何結構；在視覺端則利用 Depth-LoRA 技術結合「協同精煉模組 (SRM)」，完美實現外觀紋理（RGB）與整體結構（Depth）的雙流深度融合。在 MVTec3D-AD、Real3D-AD 等四大權威數據集上全面碾壓 PointAD，O-AUROC 平均強勢提升 1.8% 以上。
  * **解決痛點 / 推薦場景**：**完美解決了智慧製造 AOI 質檢中「商業機密與數據隱私導致缺陷樣本極度稀缺」，以及傳統單模態投影易因「光照偽影或幾何特徵微小」造成嚴重漏檢的痛點。** 無論是餅乾表面的細微凹坑，還是汽車精密零件、電纜接頭的微小劃痕，GS-CLIP 都能精確分割異常區、抑制正常區誤報，且在跨數據集（cross-dataset）遷移下效能幾乎不掉點。極度適合用於**工業精密元器件缺陷無人化柔性抽檢**、**零樣本開放世界 3A 級品管系統建構**，以及需要直接將 2D 大模型超能力無損遷移至 3D 點雲感知的工業級開發團隊。
  * **資源**：[🐙 GitHub 官方開源](https://github.com/zhushengxinyue/GS-CLIP) | [📄 官方論文 (CVF)](https://openaccess.thecvf.com/content/CVPR2026/papers/Deng_GS-CLIP_Zero-shot_3D_Anomaly_Detection_by_Geometry-Aware_Prompt_and_Synergistic_CVPR_2026_paper.pdf) | [📝 深度解讀](https://mp.weixin.qq.com/s/pbPTSgD97i-DfK_hu0SNBQ)

* **[[CVPR 2026] LAVIDA (No Need For Real Anomaly: MLLM Empowered Zero-Shot Video Anomaly Detection Framework)](https://github.com/VitaminCreed/LAVIDA)** `[2026-07-11]` 🔥
  * **核心優勢**：**徹底顛覆「先採集真實異常才能訓練」的傳統範式，首創利用語義分割數據集「現場合成偽異常」的零樣本視頻檢測史詩級神作！** 這篇由北京郵電大學與西北工業大學發佈於 CVPR 2026 的代表性工作，大膽拋棄了對真實視頻異常（VAD）數據的依賴。框架引入多模態大模型（MLLM）深厚的語義推理能力，並針對時空稀疏性創新設計「視覺 Token 逆向注意力壓縮機制」，在過濾高達 93% 冗餘背景 Token 的同時，將隱藏的異常特徵完美突出。後端串聯多尺度語義投影器與 SAM2 掩碼解碼器，直接重新定義了開放世界中的視頻幾何感知能力。
  *  **解決痛點 / 推薦場景**：完美解決了傳統安防、產線監控中「異常屬於極小機率事件、樣本收集極度困難」，以及異常定義高度依賴上下文（如奔跑在操場與在銀行含義截圖相反）的工業級痛點。 依靠「不用真實異常也能訓」的底層逻辑，模型在開放世界中展現出令人震驚的泛化實力：在 UBnormal、ShanghaiTech、UCF-Crime 與 XD-Violence 四大時序榜單上零樣本全線奪冠（XD-Violence AP 直衝 90.62%），且在 UCSD Ped2 像素級空間定位上更是以 87.68% AUC 狂勝過往 SOTA 超過 12 個百分點。極度推薦用於**開放世界無人智慧安防系統**、**多樣少量工業產線突發事故追蹤**，以及需要**極低硬體負載與抗干擾能力的多模態 Agent 視覺管線開發**。
  * **資源** Preserved：[🐙 GitHub 官方開源](https://github.com/VitaminCreed/LAVIDA) | [📄 官方論文 (arXiv:2508.03447)](https://arxiv.org/abs/2508.03447) | [📝 深度技術解讀](https://mp.weixin.qq.com/s/tvA28GTA8kzEOSkLsFvQoA)

* **[AG-VAS (Anchor-Guided Zero-Shot Visual Anomaly Segmentation)](https://github.com/xiaozhen228/AG-VAS)** `[2026-03-05]` 🔥 `[零樣本二值分割]` `[語義錨點黑科技]` `[開箱即用]` `[強泛化]`
  * **核心優勢**：**打破 CLIP 的效能天花板，首創「看一眼就知道哪裡不對勁」並直接輸出像素級二值分割掩碼的次世代大模型神作！** 這篇由中科院自動化所發佈於 CVPR 2026 的頂會工作，精準解決了傳統 AnomalyCLIP、WinCLIP 等方法「定位模糊、需要通風報信（啟發式閾值/經驗調參）」的致命硬傷。AG-VAS 在大模型詞表中革命性地擴展了三個可學習的錨點 Token (`[SEG]`, `[NOR]`, `[ANO]`)，將抽象的「孔洞、劃痕」等異常轉化為具體視覺實體，並結合「語義–像素對齊模塊 (SPAM)」完美抹平高層語意與像素特徵的巨大鴻溝，不需經驗閾值即可直接生成極致乾淨的二值化 Anomaly Mask。
  * **解決痛點 / 推薦場景**：**完美解決了工業缺陷檢測與醫療影像中「新類別樣本極度稀缺、機密隱私受限」，以及傳統多模態模型極易「混淆前景/背景與過度分割」的痛點。** 由於內建了專為分割打造的 Anomaly-Instruct20K 指令微調數據集，模型具備恐怖的跨域泛化能力——在完全未接觸醫療圖的情形下，直接越級吊打 LISA 等基線。在 MVTec-AD、KSDD2 和 ColonDB 等 6 大工業/醫學數據集上創下 AP 與 IoUano 的壓倒性 SOTA（正常圖像拒絕率高達 87.7%）。極度適合需要**零樣本、多模式互動式分割（如先描述再分割、對話中分割）**，以及追求**真正工業級、即插即用自動化質檢線**的演算法團隊。
  * **資源**：[🐙 GitHub 官方開源](https://github.com/xiaozhen228/AG-VAS) | [📄 論文 (arXiv:2603.01305)](https://arxiv.org/abs/2603.01305) | [📝 技術深度解讀](https://mp.weixin.qq.com/s/pbPTSgD97i-DfK_hu0SNBQ)

* **[UniSpector (Spectral-Contrastive Visual Prompting)](https://geonuk-kimmm.github.io/UniSpector)** `[2026-04-23]` 🔥 `[開集缺陷識別]` `[視覺提示大模型]` `[免重訓冷啟動]` `[SOTA 霸主]`
  * **核心優勢**：**打破傳統視覺提示模型的嵌入坍塌魔咒，首創「空域-頻域雙域編碼 + 角度間隔對比約束」的工業級開集缺陷識別神作！** 這項由全球電池巨頭 LG Energy Solution 發表於 CVPR 2026 的里程碑工作，直擊現有 GroundingDINO、YOLO-World 等文本/視覺提示模型在工業質檢落地時「無法對缺陷細分類、跨產品域直接失效、以及類內差異大導致特徵四散漏檢」的致命短板。UniSpector 革命性提出 SSPE 編碼器，引入 2D 傅立葉頻域分支（徑向頻譜）消除缺陷旋轉與光照偏差；並首創 CPE 對比正則模組，借鑑 ArcFace 引入角間隔損失，強制提示嵌入形成有序的「角流形」，讓同類緻密聚類、異類強制拉開。每類僅需 1~3 張提示圖即可達效能飽和，整體開集檢測 AP⁵⁰ᵇ 狂飆至 40.9%，相對最強基線（T-Rex2）暴產 19.7% 的碾壓級性能跨越！
  * **解決痛點 / 推薦場景**：**極大程度攻克了智慧製造品質管控中「產線一換批次/光源/載具模型就不穩」、未知缺陷「只能判斷異常卻無法細分類溯源維修」、以及「每次出新瑕疵都要海量標註與完整重訓」的骨灰級落地痛點。** 論文同步開源了首個視覺提示開集缺陷專用基準 **InsA**（包含 7 套數據集、360 類缺陷）。得益於推理解耦設計（提示嵌入可離線預計算快取），在線僅做目標檢測/分割，且對高斯模糊容錯與人工粗標框具備極強魯棒性。極度適合用於 **PCB / 電池片 / 金屬表面外觀的跨工位柔性檢測**、**零樣本/小樣本工業開集瑕疵隨插即用質檢線**，以及追求**兼顧已知缺陷高精度與未知缺陷強泛化**的次世代工業級 AOI 系統。
  * **資源**：[🐙 Project & Code](https://geonuk-kimmm.github.io/UniSpector) | [📄 論文 (arXiv:2604.02905)](https://arxiv.org/abs/2604.02905) | [📊 InsA 基準數據](https://geonuk-kimmm.github.io/UniSpector)

* **[ADSeeker (Knowledge-Grounded Reasoning Framework)](https://arxiv.org/pdf/2508.03088)** `[2026-07-11]` 🔥 `[多模態異常推理]` `[多模態 RAG]` `[零樣本 SOTA]` `[稀疏特徵定位]`
  * **核心優勢**：**首創結合「圖文對齊知識庫 + 鑰匙配鎖多模態檢檢索」的工業異常推理框架，為視覺大模型換上具備技術解釋力的「質檢專家大腦」！** 這項發表於 CVPR 2026 的重量級突破，徹底顛覆了傳統大模型在工業質檢中「只能看圖盲猜、定位模糊且極易產生技術幻覺」的骨灰級硬傷。ADSeeker 核心打造了 SEEK-M&V 首個圖文對齊的工業缺陷知識庫，並透過雙映射矩陣的 Q2K RAG 技術，在聯合特徵空間進行 Key-Lock 多模態精準檢索，避免傳統 RAG 視覺細節與文本語義對不齊的窘境。更驚豔的是，它採用層次化稀疏提示（HSP）搭配 $\ell_1$ 稀疏懲罰，強制模型收斂注意力、只提煉與異常強相關的特徵分量，讓零樣本異常檢測（ZSAD）在多個工業與醫學數據集上刷新全面超越前人的 SOTA 紀錄（平均 AUROC 達 94.0%）[cite: 1]。
  * **解決痛點 / 推薦場景**：**完美解決了通用多模態大模型（MLLM）在產線落地時「缺乏工業領域缺陷常識」，以及無法說出技術成因，只會無腦輸出「圖像中有一處異常」粗糙廢話的致命短板[cite: 1]。** 模型藉由 AD Expert 模組將查詢圖與正負文本做細粒度比對，產生精準的像素級異常定位分數[cite: 1]，引導解碼器給出諸如「劃痕長度、微位移成因」等老師傅等級的專家推理敘述[cite: 1]。在 MMAD 異常推理基準中，其判別與分類性能相對傳統 Qwen2.5-VL 暴力拉升[cite: 1]。由於其運算開銷較大（~28 GiB VRAM / ~6.14s），工程落地極度適合用於**需要高階邏輯推理與成因判因的離線復判、抽檢分析工站**[cite: 1]，或是作為**多 SKU、小批量且異常樣本稀缺產線的知識增強系統**[cite: 1]。
  * **資源**：[📄 論文 (arXiv)](https://arxiv.org/pdf/2508.03088) | [📊 MMAD 基準數據集](https://www.selectdataset.com/dataset/bc4b8d954262947d3ffe1370029e4eb0/MMAD)

* **[JUDO](https://github.com/woodavid31/JUDO)** `[2026-05]` 🔥
  * **核心優勢**：**打破通用大模型產線翻車魔咒，首創「對照式定位＋領域知識內化＋GRPO 推理對齊」的工業異常多模態推理器。** 這款 ICLR 2026 頂會神作基於 Qwen2.5-VL-7B 打造，徹底拋棄外掛 RAG 容易引發幻覺與邏輯偏離的弱點。它透過輸入「正常標準件與待檢件」進行視覺並置對照 (SegJux)，將工業質檢標準深植於模型權重 (DomInj)，並利用多層獎勵函數 (GRPO) 嚴格約束空間定位與工藝邏輯。在 MMAD 基準測試中，以 81.20% 的平均準確率強勢擊敗 GPT-4o。
  * **解決痛點 / 推薦場景**：**完美解決了傳統視覺大模型 (VLM) 在工業現場「看得出異常，卻給不出符合工藝邏輯的解釋」的致命痛點。** 它的輸出不再只是模糊的「合格/不合格」，而是能精準定位缺陷並解釋對裝配或密封的影響，讓 AI 推理真正可被人工複核。極度適合企業用來建構**次世代 AOI 瑕疵問答系統**、**自動化品質工程追溯 (SPC) 流程**，以及**產線專家級決策輔助大腦**，打通工業質檢的最後一哩路。<br>`[產線質檢大腦]` `[GRPO推理對齊]` `[超越GPT-4o]`
  * **資源**：[🐙 GitHub](https://github.com/woodavid31/JUDO) | [📄 論文](https://arxiv.org/abs/2605.20284) | [📝 深度解讀](https://mp.weixin.qq.com/s/7WFnkb-Vp9euyzkGLqDS2g)

* **[DCS (DINO-CLIP-SAM)](https://doi.org/10.3390/app16041836)** `[2026-06]` 🔥
  * **核心優勢**：**集結三大視覺基礎模型之大成，無需任何瑕疵樣本即可達成像素級精準分割的零樣本檢測王牌！** 這套發表於 MDPI 的創新框架，將 Grounding DINO（候選定位）、CLIP（語義感知）與 SAM（精細分割）完美串聯且完全凍結骨幹權重。透過引入細粒度文本提示 (FinePrompt)、雙路徑跨模態交互 (ADCI) 修銳異常熱力圖，以及「框＋正負點」提示組合器 (BPPC)，徹底補平了大模型間的語義斷層。在 MVTec-AD 與 VisA 基準上分別創下 94.6% 與 97.2% AUROC 的零樣本極致表現。
  * **解決痛點 / 推薦場景**：**完美解決了傳統工業質檢「異常樣本極度稀缺」，以及單純使用 CLIP/SAM 進行零樣本預測時「邊界模糊、語義歧義嚴重」的致命痛點。** 由於具備強大的開放詞彙 (Open-vocabulary) 泛化能力，極度適合**高頻換線的柔性製造產線 (High-Mix Low-Volume)**、**缺乏歷史瑕疵數據的新品試產期 (NPI) AOI 檢測**，以及作為**雲端/離線高精度瑕疵複判大腦**（需注意其串聯三大模型帶來的算力開銷，不建議用於極低延遲的邊緣設備）。<br>`[零樣本AOI]` `[大模型串聯]` `[像素級分割]` `[免微調骨幹]`
  * **資源**：[🐙 GitHub (社群實作搜尋)](https://github.com/search?q=DCS+Zero-Shot+Anomaly+Detection+DINO+CLIP+SAM) | [📄 論文](https://doi.org/10.3390/app16041836) | [📝 深度解讀](https://mp.weixin.qq.com/s/OaLdkHD1s4iQnBh-qAL3yA)

* **[AVA-DINO (Anomaly-Aware Vision-Language Adapters)](https://arxiv.org/abs/2605.12069)** `[2026-05-13]` 🔥
  * **核心優勢**：**首創「雙分支動態路由」打破零樣本適配的折衷瓶頸，徹底解耦正常與異常特徵的變換路徑！** 結合凍結的 DINOv3 與 CLIP 文本語義引導，模型不再強迫兩種樣本共用單一 Adapter，而是透過文本動態計算權重，分別強化正常特徵的「一致性」與異常特徵的「偏離性」，在 MVTec-AD 基準上飆出 93.5% 的 Image-AUROC。
  * **解決痛點 / 推薦場景**：**完美解決了真實場景中「缺陷樣本極度稀缺」且「正常/異常資料分布不對稱」的致命痛點。** 無需任何目標類別的訓練資料，即可精準應對未知瑕疵。極度推薦用於打造**高擴展性工業 AOI 質檢系統**（有效應對重疊、透明等長尾複雜缺陷）以及**跨域醫學影像檢測**（如零樣本內視鏡息肉定位）的企業級首選方案。
  * **資源**：[🐙 GitHub](https://github.com/aqeeelmirza/AVA-DINO) | [📄 論文](https://arxiv.org/abs/2605.12069)
  <br>`[零樣本檢測]` `[雙分支路由]` `[免標註質檢]` `[跨域泛化]`

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

* **[InvAD (Inversion-based Reconstruction-Free Anomaly Detection)](https://invad-project.com/)** `[2026-04]` 🔥 `[擴散模型]` `[免重建]` `[極速推論]` `[工業AOI]`
  * **核心優勢**：**徹底拋棄傳統擴散模型「加噪再去噪」的笨重重建老路，首創潛空間反演 (Latent Inversion) 評分，僅需 3 步即可狂飆 88.1 FPS 的極速判異！** 傳統擴散模型用於 AD 任務時，推論速度極慢且極度依賴噪聲強度調參 (易受產線良品波動干擾)。InvAD 革命性地改走 DDIM 潛空間反演，將模型化身為「正常分佈的尺」——不再辛苦重建影像，而是直接計算潛變量偏離正常先驗的密度。不僅實現免調參 (Tuning-free)，更支援多類別統一推論。
  * **解決痛點 / 推薦場景**：**完美解決了工業 AOI 中「擴散模型推論太慢無法跟上產線節拍」以及「反光、油污、正常加工紋路批次差導致誤檢飆高」的致命痛點。** 在最接近金屬結構件真實場景的 MPDD 資料集上，創下 96.5% 圖像級 AU-ROC 與 120 FPS 的恐怖效能。極度適合部署為**智慧工廠 24/7 產線的前級高速異常篩檢與告警**、**金屬加工件表面微小瑕疵 (劃傷/壓痕) 判異**，是真正能讓擴散模型在邊緣設備落地的工業視覺新星。
  * **資源**：[🌐 官方專案主頁](https://invad-project.com/) | [📄 官方論文 (arXiv:2504.05662)](https://arxiv.org/abs/2504.05662)

* **[AnomalyVFM (Transforming Vision Foundation Models into Zero-Shot Anomaly Detectors)](https://maticfuc.github.io/anomaly_vfm/)** `[2026-01]` 🔥 `[零樣本冷啟動]` `[純視覺VFM]` `[虛擬產線數據]` `[極速推論]`
  * **核心優勢**：**打破 CLIP 語言提示的局限，首創將純視覺大模型 (VFM) 轉化為零樣本工業檢測霸主的黑科技！** 徹底拋棄傳統視覺語言模型 (VLM) 依賴文字描述缺陷的弱點（文字往往難以精準描述微小劃傷或紋理斷裂）。AnomalyVFM 創新採用 FLUX 合成並透過 DINOv2 嚴格過濾的「虛擬產線」缺陷數據，搭配深層注入 Transformer 的 LoRA 低秩適配器。在 9 大工業數據集上創下 94.1% 圖像級 AUROC 的驚人成績，且 A100 單卡推論僅需 20.5ms，速度與精度全面輾壓 Bayes-PFL 等對手。
  * **解決痛點 / 推薦場景**：**完美解決工業 AOI 產線頻繁換料號、換工藝時「完全沒有瑕疵樣本可訓練」的冷啟動致命痛點。** 它直接從強大的純視覺骨幹 (如 RADIO, DINOv3) 中萃取對「不尋常紋理與邊緣形變」的敏銳度。極度適合部署為**智慧工廠新產線的首檢預篩與異常告警系統**、**多品類/小批量 (High-Mix Low-Volume) 的柔性製造視覺大腦**，以及要求極高節拍與低延遲的**邊緣運算質檢站**。
  * **資源**：[🐙 GitHub 官方源碼](https://github.com/maticfuc/anomaly_vfm) | [📄 官方論文 (arXiv:2601.20524)](https://arxiv.org/abs/2601.20524) | [🌐 專案主頁](https://maticfuc.github.io/anomaly_vfm/)

* **[[ICCV 2025] TF-IDG (Training-Free Industrial Defect Generation with Diffusion Models)](https://openaccess.thecvf.com/content/ICCV2025/papers/Xu_Training-Free_Industrial_Defect_Generation_with_Diffusion_Models_ICCV_2025_paper.pdf)** `[2025-10]` 🔥 `[免訓練黑科技]` `[One-Shot資料增廣]` `[產線冷啟動]` `[台灣原生強權]`
  * **核心優勢**：**徹底終結傳統瑕疵生成依賴大量樣本與微調的宿命，首創「免訓練、單張參考圖」即可量產高保真瑕疵數據的工業級救星！** 由國立臺灣大學資工系與華碩團隊聯手發表的 ICCV 2025 重量級神作。該技術完全不需要對擴散模型進行任何權重微調，純粹在推理階段透過創新的 Sinkhorn 特徵對齊策略（最優傳輸理論）與自適應缺陷遮罩引導機制（AAM），精準復現精密工件如 PCB、晶體管等細長或微米的複雜缺陷細節。同時，內建的雙路紋理保持模組（TP）消除了邊緣「貼圖感」，讓生成的瑕疵與背景自然光影完美融合。
  * **解決痛點 / 推薦場景**：**完美解決了智慧製造與自動光學檢測（AOI）產線在料號切換、冷啟動初期「完全沒有缺陷樣本可供訓練模型」的產線頭號痛點。** 過去的方法至少需要幾十張圖來微調 GAN 或 LoRA，而 TF-IDG 在 1-shot（僅一張良品底圖＋一張瑕疵參考圖）設定下，下游分類模型的準確率就直接暴漲 20+ 個百分點，越少樣本優勢越恐怖。生成的影像自帶高精度 Mask，可隨插即用地接入 YOLO、U-Net 或 GLASS 等主流檢測模型，是打造**柔性製造智慧工廠**、**小批量多 SKU 工檢平台**，以及需要**算力門檻極低、消費級顯卡就能跑的純本地私有化資料清洗與增廣管線**的工業級大腦首選。
  * **資源**：[🐙 GitHub 官方開源](https://github.com/rubymiaomiao/TF-IDG) | [📄 官方論文 (PDF)](https://openaccess.thecvf.com/content/ICCV2025/papers/Xu_Training-Free_Industrial_Defect_Generation_with_Diffusion_Models_ICCV_2025_paper.pdf)

* **[FastRef (Fast Prototype Refinement for Few-shot Industrial Anomaly Detection)](https://github.com/liyufei25/FastRef)** `[2026-03-29]` 🔥
  * **核心優勢**：**首創「特徵遷移 + 異常抑制」雙向迭代嵌套優化框架，推理階段 2 輪迭代即時收斂的少樣本隨插即用神作！** 這項發表於 CVPR 2026 的前沿成果，徹底打破了傳統 PatchCore、WinCLIP 等方法在冷啟動階段高度依賴「靜態原型」而導致未知缺陷重構偏差變小、進而頻繁漏檢的局限性。FastRef 創新地在推理階段動態引入查詢影像（Query Image）的統計特徵，一邊透過具備閉式解（closed-form）的變換矩陣 W 進行高效特徵遷移，一邊利用最優傳輸（Optimal Transport）演算法中的 Sinkhorn 迭代，精準激活異常區域權重並進行「避障式更新」，完美剔除不符合正常分佈的污染特徵。
  * **解決痛點 / 推薦場景**：**完美解決了工業自動化質檢產線在「冷啟動階段、樣本極度稀缺」時，傳統靜態原型易被瑕疵干擾、背景誤報率高且邊緣勾勒模糊的痛點。** 該演算法最具破壞性的賣點在於其**工業級的高相容性與即插即用（Plug-and-Play）特質**，能直接無痛嵌入 PatchCore、WinCLIP、AnomalyDINO 等主流管線。實測在 MVTec、MPDD、ViSA 等四大權威資料集上的 1/2/4-shot 評測中全面洗榜，在複雜的 ViSA 場景下更創下 Image-AUROC +7.3% 的驚人跨越。極度適合用於**多樣少量生產線的柔性缺陷初篩**、**新品上線的少樣本極速部署**以及對推論即時性有嚴苛要求的**邊緣運算即時 AOI 質檢管線**。
  * **資源**：[🐙 GitHub](https://github.com/liyufei25/FastRef) | [📄 論文](https://arxiv.org/abs/2603.01305) *(註：實際 arXiv 連結請以官方發布為準)* | [📝 深度解讀](https://mp.weixin.qq.com/s/kiZLqZupxWTB8nB-2bzU6w)

* **[FoundAD (少樣本異常檢測基礎編碼器)](https://arxiv.org/abs/2510.01934)** `[2025-10]` 🔥
  * **核心優勢**：**打破工業質檢對提示詞與重型解碼器的依賴，僅靠輕量投影器徹底釋放視覺大模型「天生」的異常感知力！** 慕尼黑工業大學與 MVTec 聯合發布的 ICLR 2026 神作。它證明了凍結的 DINOv2/v3 特徵空間本身就隱含「自然圖像流形」，只需外掛一個僅 11.8M 參數的輕量非線性投影器，即可將偏離流形的特徵拉回並計算殘差分數。完全不需文字提示 (Prompt) 或龐大記憶庫，在 MVTec-AD 1-shot 設定下飆出 96.1% I-AUROC，且單卡推理高達 7.8 FPS，顯存佔用不到 1.4GB。
  * **解決痛點 / 推薦場景**：**完美解決了真實工業場景中「缺陷樣本極難取得」、「CLIP 提示詞工程過於脆弱」以及「傳統重建解碼器過於龐大難以落地」的三大致命痛點。** 由於其極致的輕量化與純視覺特徵空間運算特性，極度推薦用於**資料極度稀缺的產線新品瑕疵檢測**、**高頻流水線的即時 AOI 邊緣運算 (Edge AI)**，以及不允許複雜微調的**跨場景柔性製造檢測系統**，是目前工業級落地 SOTA 的最高 CP 值選擇。
  * **資源**：[🐙 GitHub 官方開源](https://github.com/ymxlzgy/FoundAD) | [📄 arXiv 論文](https://arxiv.org/abs/2510.01934) | [🌐 OpenReview (ICLR 2026)](https://openreview.net/forum?id=YRrlJ8oVEH)
  <br>`[1-shot極限檢測]` `[免文字提示]` `[極低顯存]` `[工業AOI]`

* **[MeDS](https://github.com/SirojbekSafarov/MeDS)** `[2026-05]` 🔥
  * **核心優勢**：**打破工業質檢「訓練集必須絕對乾淨」的不可能假設，首創無懼 40% 髒數據污染的自清洗抗噪異常檢測框架！** 這篇 ICML 2026 的強悍之作直擊產線最痛的「標籤噪聲」現實。透過「自舉稀疏記憶庫 (Bootstrapped Memory) 粗篩」、「記憶分數蒸餾 (Score Distillation) 細化定位」與「漸進式樣本選擇 (Progressive Selection) 閉環微調」三步法，讓模型自己學會過濾異常。在 MVTecAD 基準測試中，即便訓練集混入高達 40% 的瑕疵樣本，它依然能將 I-AUROC 從崩潰邊緣的 87.38% 強勢拉回 99.16%，展現驚人的魯棒性。
  * **解決痛點 / 推薦場景**：**完美解決了真實工廠中因「輕微缺陷漏標、加工紋理波動、多人標註口徑不一」導致模型決策邊界變寬容、上線後漏檢率飆升的致命痛點。** 它並非要取代現有的 UAD 模型 (如 Dinomaly)，而是作為一層可插拔的「抗污染保險層」掛載於現有架構上。極度適合**數據維護與清洗成本極高的傳統製造業**、**特徵變異大的機加工/鑄造/焊接產線**，以及作為**協助 QC 工程師優先篩檢可疑髒數據的自清洗前置模組**。<br>`[工業抗噪神作]` `[無懼髒數據]` `[自清洗閉環]` `[產線落地首選]`
  * **資源**：[🐙 GitHub](https://github.com/SirojbekSafarov/MeDS) | [📄 論文](https://arxiv.org/abs/2605.26676)

* **[Boxes2Pixels (框標註轉像素級分割神作)](https://arxiv.org/abs/2604.11162)** `[2026-04]` 🔥
  * **核心優勢**：**CVPR 2026 工業視覺革命！首創「單向自糾正」機制，僅靠廉價的「框標註 (Bounding Box)」即可榨出 SOTA 級的像素級缺陷分割！** 巧妙利用 SAM 生成偽標籤，並透過「全局 DINOv2 語意 + 局部 CNN 細節」的雙分支層次化學生架構，完美過濾大模型生成的系統性雜訊與漏檢。可訓練參數暴降 80% (僅 5.6M)，推理速度飆破 161 FPS。
  * **解決痛點 / 推薦場景**：**完美解決了工業 AOI 領域「像素級標註成本極高（耗時且需專家知識）」且「細長裂紋、低對比凹陷難以精準定位」的致命痛點。** 企業無需重新耗時塗抹缺陷邊緣，直接沿用舊有的 YOLO 框標註資料庫即可無痛升級為高精度分割模型。極度推薦用於**風機葉片微小裂紋檢測**、**高頻流水線表面污損剔除**，以及算力受限的**即時邊緣運算質檢設備 (Edge AI)**，是產線自動化升級的超高性價比方案。
  * **資源**：[🐙 GitHub](https://github.com/CLendering/Boxes2Pixels) | [📄 論文](https://arxiv.org/abs/2604.11162)
  <br>`[弱監督分割]` `[免像素標註]` `[極速161FPS]` `[工業AOI]`

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

* **[Uni-RCM (跨模態多類別統一異常檢測框架)](https://arxiv.org/abs/2605.29455)** `[2026-05]` 🔥
  * **核心優勢**：**打破「一類產品養一套模型」的產線維護惡夢，首創跨模態統一建模的工業質檢神作！** 徹底拋棄傳統容易導致特徵混疊的龐大 Memory Bank，創新引入「參考引導塊 (Reference Guide Block)」為多類別特徵提供一個穩定的跨模態錨點，動態過濾類別雜訊。此外，透過「離線殘差量化器 (ORQ)」以緊湊的小碼本 (Cascaded Codebooks) 約束正常特徵流形。在 MVTec 3D-AD 的多類別統一檢測基準中，其 I-AUROC 狂飆至 95.4%，強勢輾壓現有 SOTA 方法。
  * **解決痛點 / 推薦場景**：**完美解決了真實產線中「多種物料與治具混線生產」導致模型數量無限膨脹、版本回歸與更新成本極高的致命痛點。** 透過 2D RGB (紋理表面) 與 3D 點雲 (幾何結構) 特徵的乘法互補融合，能同時精準抓出微小刮傷與立體結構變形。極度適合**多樣少量柔性製造 (Flexible Manufacturing)** 產線，以及企圖以**單一 AI 底座支援全廠多品項**的次世代企業級 AOI 視覺質檢系統。
  * **資源**：[📄 arXiv 論文 (2605.29455)](https://arxiv.org/abs/2605.29455) | [📝 微信公眾號深度解讀](https://mp.weixin.qq.com/s/G2AtBBpeh2qkTffw-ik5Tg)
  `[統一建模]` `[跨模態對齊]` `[AOI工業視覺]` `[多類別部署]`

* **[MOCHA](https://www.alphaxiv.org/zh/overview/2509.14001v1)** `[2025-09-20]`：Multi-modal Objects-aware 架構。將此技術注入 YOLO 後，檢測效能獲得大幅度成長。[📝 中文解讀](https://zhuanlan.zhihu.com/p/1952054591035281418)
* **[FS-SAM2](https://zread.ai/fornib/FS-SAM2)** `[2025-09-24]`：將 Meta 的 SAM 2 (Segment Anything 2) 模型適配於少樣本語義分割任務，在效能與效率上達到雙優。

---

## ObjectDetection
**🎯 Object Detection (目標偵測)**

> **YOLOv11 架構在邊緣設備上的推論效能達到全新里程碑。** 在 NVIDIA Jetson Orin 平台上實測，其 mAP 達 54.3% 時仍可維持 120 FPS 的即時處理速度。這為自駕車與高頻工業自動化提供了延遲小於 10ms 的完美解決方案。目標偵測不僅是畫出邊界框 (Bounding Box)，目前的趨勢是結合語言模型與強化學習，實現「開放詞彙 (Open-Vocabulary)」與「極端場景特化」。

* **[SAM 3D (3Dfy Anything in Images)](https://github.com/facebookresearch/sam-3d-objects)** `[2026-05]` 🔥 `[單圖3D重建]` `[SAM家族升維]` `[DPO對齊]` `[亞秒級極速生成]`
* **核心優勢**：**打破 2D 到 3D 的數據壁壘，單張照片秒建高品質、可互動的三維場景！** Meta 於 CVPR 2026 榮獲提名的劃時代神作，將「分割萬物 (SAM)」的感知能力正式升維至 3D 空間。完美借鑑大語言模型 (LLM) 的「預訓練 → 真實數據微調 → DPO 偏好對齊」三階段煉丹法，結合 DINOv2 語意與稀疏潛流匹配 (Sparse Latent Flow)。模型不僅能像人類一樣「腦補」物體被遮擋的背面幾何形狀，還能精準還原高保真材質紋理。更透過模型蒸餾將推理極限壓縮至 4 步，達成驚人的亞秒級極速重建。
* **解決痛點 / 推薦場景**：**完美解決了傳統 3D 生成「極度依賴多視角拍攝」，且「遇到真實雜亂場景 (In-the-wild) 容易穿模、幾何崩壞」的致命痛點。** 模型原生支援輸出通用三角網格 (Triangle Mesh) 與 3D 高斯潑濺 (3DGS)，能無縫導入 Blender、Maya 與現代主流遊戲引擎。極度適合**遊戲與 XR 開發團隊進行 3D 資產極速量產**、賦予**具身智能機器人 (Embodied AI)** 空間幾何的直覺感知，以及作為**自駕車複雜場景理解**的工業級 3D 基礎模型。
* **資源**：[🐙 GitHub 官方開源 (Objects)](https://github.com/facebookresearch/sam-3d-objects) | [📄 官方論文 (arXiv:2511.16624)](https://arxiv.org/abs/2511.16624) | [🌐 官方專案與線上 Demo](https://ai.meta.com/sam3d/)

* **[MonoSAOD (Monocular 3D Object Detection)](https://github.com/VisualAIKHU/MonoSAOD)** `[2026-04]` 🔥 `[單目3D偵測]` `[稀疏標註]` `[偽標籤治理]` `[工業級過濾]`
  * **核心優勢**：**打破低標註場景的「雜訊污染」魔咒，首創物理感知增強與嚴苛偽標籤篩選的單目 3D 偵測神作！** 徹底推翻了過往半監督學習「高置信度即為好標籤」的盲點。透過獨創的 RAPA 模組，確保生成的 3D 幾何、尺度與空間關係完全符合現實物理約束；並利用 PBF (偽標籤緩衝過濾器) 作為「數位復檢工位」，嚴格把關深度不確定性與原型一致性，在僅有 30% 標註數據的極限下，效能強勢輾壓傳統 Co-student 等算法。
  * **解決痛點 / 推薦場景**：**完美解決了真實工業 AOI 與自駕感知中「標註成本極高」，且「錯誤偽標籤進入訓練閉環導致模型越練越崩潰」的致命痛點。** 它的核心落地價值在於「資料治理的工程化」——不盲目擴充髒數據，而是確保餵給模型的每一筆資料都乾淨且物理自洽。極度適合**樣本極度稀缺的工業裝配/幾何公差檢測**、**單目相機 3D 測距與姿態估計**，以及**低成本自駕車邊緣感知系統**。
  * **資源**：[🐙 GitHub 官方專案](https://github.com/VisualAIKHU/MonoSAOD) | [📄 官方論文 (arXiv:2604.01646)](https://arxiv.org/abs/2604.01646)

* **[LocateAnything-3B (全能視覺定位與多模態檢測)](https://github.com/NVlabs/Eagle)** `[2026-05]` 🔥
  * **核心優勢**：**NVIDIA 顛覆視覺定位的 CVPR 2026 神作！首創「平行框解碼 (PBD)」徹底打破大模型自迴歸生成座標的龜速與誤差，單卡 H100 狂飆 12.7 BPS！** 捨棄傳統將座標拆成 Token 逐一生成的作法，LocateAnything 將邊界框視為不可分割的「幾何原子單元」一步到位預測。結合高達 7.85 億的巨量邊界框訓練標註與獨創的 Hybrid 模式（在極速並行與嚴謹自迴歸間動態切換、遇錯重解），在 UI 元素定位與 LVIS 高精度基準上強勢輾壓 Qwen3-VL 與 Rex-Omni。
  * **解決痛點 / 推薦場景**：**完美解決了傳統視覺大模型 (VLM) 應用於 AI Agent 與具身智能時「看得懂卻找得極慢、座標框亂跳前後矛盾」的致命痛點。** 僅 3B 參數，只需 16GB 消費級顯存（如 RTX 3090/4090）即可流暢本地部署。極度推薦開發者用於打造毫秒級反應的**電腦操作智能體 (Computer Use Agent)**、**精準點擊 UI 的 RPA 自動化導航副駕**，以及需要極低延遲的**具身機器人 (Embodied AI) 視覺抓取中樞**。
  * **資源**：[🐙 GitHub](https://github.com/NVlabs/Eagle) | [📄 論文](https://research.nvidia.com/labs/lpr/locate-anything/LocateAnything.pdf) | [🤗 HF 權重](https://huggingface.co/nvidia/LocateAnything-3B) | [🌐 線上 Demo](https://huggingface.co/spaces/nvidia/LocateAnything)
  <br>`[平行框解碼]` `[UI自動化導航]` `[具身智能]` `[極低延遲]`

* **[DetAny4D (端到端 4D 開放集物體檢測基準)](https://arxiv.org/abs/2511.18814)** `[2026-02]` 🔥
  * **核心優勢**：**打破串流影片 3D 檢測的「逐幀抖動」魔咒，首創端到端 (End-to-End) 的 4D 開放集全域感知黑科技！** 徹底拋棄傳統「先檢測後追蹤 (Detect-then-Track)」的複雜級聯管線。透過全新設計的「幾何感知時空解碼器 (Spatiotemporal Decoder)」，模型能一次性從 RGB 串流影片中預測出跨幀極度穩定、全域時空一致的 3D 邊界框 (Bounding Box)。團隊更同步釋出了包含 28 萬筆序列的專用巨型資料庫 DA4D 來解決 4D 訓練資料荒。
  * **解決痛點 / 推薦場景**：**完美解決了傳統單幀 3D 檢測在動態影片中「邊界框狂抖、同一物件身分跳變」，以及依賴複雜關聯演算法導致「誤差一路放大傳染」的致命痛點。** 實測在 DA4D 基準上將跨幀變異數 (Variance) 暴力壓低 10%~30%，且 3D 精度絲毫不減。極度推薦用於打造**自動駕駛連續環境感知系統**、**具身智能 (Embodied AI) 動態軌跡預測**，以及需要長期穩定推理的**串流影片空間計算**場景。
  * **資源**：[🐙 GitHub (即將開源)](https://github.com/jarvishou829/DA4D/) | [📄 官方論文](https://arxiv.org/abs/2511.18814) | [🌐 DA4D 專案主頁](https://jarvishou829.github.io/DA4D/)
  <br>`[4D物件偵測]` `[開放集 Open-set]` `[時空一致性]` `[自駕車感知]`

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

* **[SEATrack (Simple, Efficient, and Adaptive Multimodal Tracker)](https://openaccess.thecvf.com/content/CVPR2026/papers/Su_SEATrack_Simple_Efficient_and_Adaptive_Multimodal_Tracker_CVPR_2026_paper.pdf)** `[2026-06]` 🔥 `[多模態追蹤]` `[PEFT極致輕量]` `[極端場景特化]` `[邊緣算力首選]`
  * **核心優勢**：**打破多模態追蹤參數暴漲的死局，僅需 0.6M 可訓練參數即霸榜 CVPR 2026 的極速跟蹤神作！** 徹底推翻傳統「盲目堆疊融合模塊」的套路，首創「先對齊後融合」的新範式。透過僅 0.14M 參數的 AMG-LoRA 動態對齊 RGB 與其他模態（熱紅外/深度/事件）的匹配響應，消除了跨模態注意力衝突；並結合 HMoE 分層混合專家模塊實現高效全局建模。推論速度高達 63.5 FPS，顯存僅需 1GB，效能卻強勢輾壓參數量大 25 倍的對手 (如 SDSTrack)。
  * **解決痛點 / 推薦場景**：**完美解決純 RGB 視覺在「夜間、強光、大霧」等惡劣天候下容易死機跟丟，以及傳統多模態模型「吃顯存、容易引發災難性遺忘」的致命痛點。** 面對目標短暫離開視野 (OV) 或幀丟失 (FL)，其自適應互引導機制能瞬間用可靠模態補位。極度適合部署於算力嚴苛的**無人機 (UAV) 惡劣天候全天候巡檢**、**自駕車夜視感知大腦**，以及**軍工級熱紅外線目標鎖定與安防追蹤系統**。
  * **資源**：[📄 CVPR 2026 官方論文](https://openaccess.thecvf.com/content/CVPR2026/papers/Su_SEATrack_Simple_Efficient_and_Adaptive_Multimodal_Tracker_CVPR_2026_paper.pdf) | [🔍 GitHub 潛在開源搜尋](https://github.com/search?q=SEATrack+Multimodal+Tracker)

* **[FT-FSOD (Parallel Decoder)](https://github.com/Intellindust-AI-Lab/FT-FSOD)** `[CVPR 2026]` 🔥 `[跨域少樣本]` `[並行解碼器]` `[自動化微調]`
  * **核心優勢**：**打破跨域微調的過度擬合魔咒，僅靠輕量解碼器魔改與漸進式微調，強勢輾壓 SAM 3！** 論文證實，面對巨大域偏移（如工業瑕疵、醫療影像），一味把模型做大是錯的！透過首創的「混合集成解碼器 (HED)」引入並行預測多樣性，搭配 plateau-aware 漸進式微調策略，幾乎**零額外參數**即可徹底解決少樣本訓練極易震盪與收斂困難的致命缺陷。
  * **解決痛點 / 推薦場景**：**完美解決傳統視覺模型導入特殊產業（如工業 AOI 缺陷、空拍圖、水下探勘或文件解析）時，因「標註資料極少」加「場景差異過大」導致模型泛化能力直接崩潰的痛點。** 實測在包含 100 個極端異構資料集的 RF100-VL 基準上，10-shot 效能 (41.9 mAP) 顯著擊敗 SAM 3 與 DINO 家族。極度適合沒有海量算力與標註人力、不想手動痛苦調參，卻需要讓 AI 快速適配陌生新場景的企業級跨域目標檢測任務。
  * **資源**：[🐙 GitHub 官方開源](https://github.com/Intellindust-AI-Lab/FT-FSOD)

* **[Rex-Omni](https://rex-omni.github.io/)** `[CVPR 2026]` 🔥 `[檢測一切]` `[GRPO強化學習]` `[Qwen2.5-VL底座]`
  * **核心優勢**：**打破語言理解與視覺定位的壁壘，首創引入 GRPO 強化學習的「檢測一切」多模態大模型！** 基於 3B 輕量級 Qwen2.5-VL 打造，徹底拋棄傳統 YOLO/DETR 依賴的座標迴歸（Regression），將目標偵測、OCR、GUI 定位與關鍵點提取，全部霸氣統一為「離散座標序列預測」任務。透過獨創的幾何感知獎勵函數（GRPO）進行後訓練，精準糾正了以往多模態模型（MLLM）常見的座標漂移與重複預測問題。
  * **解決痛點 / 推薦場景**：**完美解決了傳統視覺大模型「看得懂複雜指令，卻框不準精確位置」的致命痛點。** 它的零樣本 (Zero-shot) 檢測效能直接匹敵甚至超越 Grounding DINO 等專用模型。極度適合用於開發需要深度語言理解的**自動化 GUI 網頁操作代理 (Web Agent)**、**複雜圖表/排版的 OCR 系統**，以及支援自然語言指令的**開放詞彙 (Open-Vocabulary) 機器人視覺感知系統**。
  * **資源**：[🐙 專案首頁與程式碼](https://rex-omni.github.io/) | [📄 arXiv 論文](https://arxiv.org/abs/2510.12798)

* **[YOLO26 頻域增強版 (FrequencyCM × C3k2)](https://arxiv.org/abs/2509.25164)** `[2025-09]` 🔥
  * **核心優勢**：**首創「頻域增強」打破空間卷積天花板，YOLO26 透過端到端無 NMS 設計達成邊緣設備的極速推論！** 將 UCMNet 的頻率卷積模組 (FCM) 巧妙植入 C3k2，結合 STAL 小目標標籤分配與 MuSGD 優化器，以極低的計算開銷取得整圖級全局感受野。同時透過架構「做減法」(直接移除 DFL 與 NMS)，大幅降低 ONNX/TensorRT 的導出摩擦與延遲。
  * **解決痛點 / 推薦場景**：**完美解決了傳統物件偵測模型「部署後處理繁瑣」且「面對低解析、模糊與小目標時高頻細節嚴重丟失」的致命痛點。** 無需再依賴手動調參的 IoU 閾值，極度適合**硬體資源受限的邊緣運算設備 (如 Jetson Nano、無人機)**，更是打造**工業級紅外線缺陷檢測**、**低對比度醫學影像分析**與複雜場景即時目標跟蹤的工業級首選黑科技。
  * **資源**：[📄 論文](https://arxiv.org/abs/2509.25164) 
  <br>`[端到端無NMS]` `[頻域增強]` `[小目標檢測]` `[極低延遲部署]`

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

> **零樣本 (Zero-shot) 分割模型徹底改變了醫療與遙測影像的標註流程。** 應用 SAM (Segment Anything Model) 架構，可將多邊形標註時間從平均 3 分鐘縮減至 2 秒內，整體人力成本驟降 85%，且維持與人工標註達 95% 的 IoU 重合度。自從 Meta 推出 Segment Anything (SAM) 以來，圖像分割已經進入「提示即分割 (Promptable Segmentation)」的時代。

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

* **[VGGT-S (VGGT-Segmentor)](https://github.com/buaa-colalab/VGGT-S)** `[2026-04]` 🔥 `[跨視角分割]` `[幾何增強]` `[Ego-Exo對齊]` `[免配對預訓練]`
  * **核心優勢**：**打破多視角像素匹配的漂移魔咒，首創將「幾何點投影」作為粗提示的跨視角分割神作！** 這篇由北航發表的 CVPR 2026 Oral 論文，巧妙地避開了直接進行像素級匹配易失效的陷阱。它凍結了強大的 VGGT 幾何基礎模型編碼器，不強求精確的點對點對齊，而是將投影點當作「幾何錨點提示 (Geometric Prompts)」，再搭配輕量級的聯合分割頭 (Union Segmentation Head) 進行特徵融合與遮罩細化 (Mask Refinement)。在無配對數據 (Correspondence-free) 預訓練下，IoU 效能依然狂碾 DOMR 等現有 SOTA 超過 10 幾個百分點。
  * **解決痛點 / 推薦場景**：**完美解決了「第一人稱 (Ego) 視角極易被手部遮擋」與「第三人稱 (Exo) 視角目標過小且背景相似物干擾多」，導致傳統模型在跨視角轉換時形狀崩壞的致命痛點。** 只要給定一個視角的目標遮罩，模型就能靠著空間幾何直覺，在另一個截然不同的視角精準框出同一物體。極度推薦給開發**具身智能機器人 (Embodied AI) 模仿學習與雙臂操作**、**AR/VR 遠端專家空間協作系統**，以及需要多相機聯合感知的**無人機與地面視角協同監控**的工程團隊。
  * **資源**：[🐙 GitHub 官方開源](https://github.com/buaa-colalab/VGGT-S) | [📄 官方論文 (arXiv:2604.13596)](https://arxiv.org/abs/2604.13596)

* **[DiCLIP (Diffusion Enhanced CLIP for Weakly Supervised Segmentation)](https://github.com/zwyang6/DiCLIP)** `[2026-06]` 🔥 `[弱監督分割 WSSS]` `[知識遷移]` `[訓練降本 90%]` `[生成式賦能]`
  * **核心優勢**：**徹底終結弱監督語義分割「只亮核心局部、邊界殘缺不全」的先天盲區，用 1/10 的訓練成本逼近全監督 96.6% 的效能極限！** 復旦大學團隊最新力作，精準指出傳統 CLIP 偏向全局語意、缺乏像素空間細節的「近視眼」痛點。DiCLIP 革命性地將 Stable Diffusion (SD) 的 self-attention map 視為天然的空間老師，首創 ACR 遞歸精化與 VCE 視覺增強機制，將豐富的幾何局部一致性注入 CLIP 中。同時利用 SD 離線生成單類別乾淨圖像建立 Key-Value Cache 視覺知識庫，將傳統的 patch-text 對齊強勢升級為「視覺檢索範式」。
  * **解決痛點 / 推薦場景**：**完美解決了傳統弱監督分割 (WSSS) 依賴海量像素級 Mask 標註導致「成本高昂、冷啟動極慢」的工業致命痛點。** 由於 SD 全程凍結且不參與重訓，整體線上訓練時間暴砍至 WeCLIP 的 42.6% 與 WeakCLIP 的 9.9%，在單張消費級顯卡上即可極速收斂（4.8G 顯存、115 分鐘完訓）。極度適合需要**低成本快速原型驗證的語義分割專案**、缺乏人工標註心力的**自動駕駛開放世界邊緣案例感知**，以及探索**「生成式模型賦能基礎視覺模型」**的次世代多模態研究。
  * **資源**：[🐙 GitHub](https://github.com/zwyang6/DiCLIP) | [📄 論文](https://arxiv.org/abs/2606.23050) *(註：實際 arXiv 頁面依官方為準)*

* **[CaptionFormer](https://www.gabriel.fiastre.fr/captionformer/)** `[2026-06]` 🔥
  * **核心優勢**：**首創端到端整合「像素級分割、跨幀追蹤與自然語言描述 (DVOC)」的統一架構，並神來一筆運用 VLM (Gemini 2.0) 自動合成海量影片軌跡標註，將訓練成本狂降至傳統方法的十分之一 (僅需 ~208 GPU hours)！** 巧妙地將缺乏描述的 LVIS/LV-VIS 標註轉化為高品質的時空軌跡數據集，讓模型在單一管線中學會精準的「時間與物理一致性」。
  * **解決痛點 / 推薦場景**：**完美解決了傳統影片理解任務中「人工逐幀標註成本爆炸」與「多模組拼接（檢測+追蹤+生成分開做）導致時空語意斷層」的致命痛點。** 藉由創新的時序聚合 (Temporal Aggregation) 技術，模型能精確掌握同一個物體「在哪裡、去了哪、正在做什麼」。是打造**零樣本長影片語意檢索 (Zero-shot Video Retrieval)**、**機器人動態場景感知**、**高階智慧安防監控**與**互動式 AI 影片編輯**的次世代神作。

* **[SAM3-LoRA 醫學影像微調實戰 (ISIC 2018)](https://github.com/little51/dinov3-course)** `[2026]` 🔥
  * **核心優勢**：**打破通用大模型在專業領域「水土不服」的魔咒，6GB 顯存即可實現 SAM3 的極速領域特化！** 針對 SAM3 在醫療影像上零樣本能力低下的問題，捨棄昂貴的全參數訓練，導入 LoRA 技術僅微調 0.43% 的關鍵參數 (Q/V/K/Out)。並創新結合「邊界框 (Bounding Box) 提示詞」自動對齊策略，僅需 1 輪訓練即可將皮膚癌病灶的 Dice 係數由 0.892 暴升至 0.943，大幅提升邊緣輪廓的精準度。
  * **解決痛點 / 推薦場景**：**完美解決了將視覺大模型 (VFM) 導入特殊產業時「缺乏自然語言提示詞」以及「全量微調算力門檻過高 (需 12GB+ 顯存)」的致命痛點。** 此開源管線為開發者提供了標準化的二次開發路徑，後續更可無縫串聯 YOLO 等目標偵測模型，實現「先檢測、後精細分割」的全自動化流水線。極度適合**醫療病灶高精度輔助診斷**、**工業 AOI 複雜瑕疵提取**，以及缺乏龐大 GPU 算力的**個人開發者與學術研究團隊**。
  * **資源**：[🐙 GitHub 完整微調源碼](https://github.com/little51/dinov3-course) | [📝 SAM3 微調技術深度解析](https://blog.csdn.net/little51/article/details/145892552)
  `[SAM3微調]` `[醫療影像特化]` `[低算力救星]` `[LoRA極速煉丹]`

* **[X2SAM](https://github.com/wanghao9610/X2SAM)** `[2026-05]` 🔥 `[圖影大一統]` `[多模態分割]` `[時序一致性]`
  * **核心優勢**：**終結圖像與影片分割割裂的全新範式，單一模型包辦 14 項分割任務的通用視覺大腦！** 結合 Qwen3-VL 的語意理解與 SAM2 的精準分割，X2SAM 首次在單一框架內同時支援圖像/影片雙輸入與文字/視覺（點、框）雙提示。其獨創的 **Mask 記憶模組 (Mask Memory Module)** 作為短期視覺工作記憶，在影片推理分割 (V-Rea. Seg.) 上狂飆提升 14.2 個百分點，強勢刷新 SOTA。
  * **解決痛點 / 推薦場景**：**完美解決了過往模型「只能做圖或只能做影片」的架構碎片化痛點，以及影片分割中常見的物體身份跳變與閃爍問題。** 透過 6 幀的 FIFO 記憶機制保持極高的時序一致性。極度適合用於開發**全能型具身智能 (Embodied AI) 連續環境感知系統**、**高互動性影視特效自動摳圖**，以及需要精準追蹤動態目標的**安防監控與自駕車視覺**。
  * **資源**：[🐙 GitHub](https://github.com/wanghao9610/X2SAM) | [📄 論文](https://arxiv.org/abs/2605.00891) | [🌐 專案主頁](https://wanghao9610.github.io/X2SAM)

* **[BCSI (Bidirectional Channel-selective Semantic Interaction)](https://arxiv.org/abs/2601.05855)** `[2026-01]` 🔥
  * **核心優勢**：**AAAI 2026 醫學影像分割神作！首創「雙向通道級交互」徹底打破半監督學習的誤差累積與特徵同質化瓶頸。** 捨棄臃腫的多分支架構，採用極簡單編碼器設計，並導入「語義–空間雙維度擾動」與動態通道選擇路由 (CR)。它能精準篩選出高價值的特徵通道，讓標註與未標註資料進行高純度、無雜訊的雙向信息交換，在 BraTS-2019 (腦腫瘤) 僅用 20% 標註資料，表現便超越全量標註的全監督模型！
  * **解決痛點 / 推薦場景**：**完美解決了臨床醫學影像「像素級標註成本極高（需耗費醫師大量時間）」且「傳統半監督模型極易受偽標籤雜訊干擾而崩潰」的致命痛點。** 極度推薦用於打造**企業級 AI 醫療輔助診斷系統**、**複雜 3D 微小器官精準定位**（如難度極高的胰臟分割），是醫療 AI 演算法團隊在極少數標註資源下，榨出臨床級高精度的工業級首選黑科技。
  * **資源**：[🐙 GitHub](https://github.com/taozh2017/BCSI) | [📄 論文](https://arxiv.org/abs/2601.05855) 
  <br>`[半監督學習]` `[醫學影像分割]` `[雙向通道交互]` `[免大量標註]`

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

> **多模態大模型 (MLLM) 已成為高複雜度文檔解析的標準配置。** 結合 MinerU 或 DeepSeek-VL，針對手寫體與多語言混排表單的辨識準確率突破 96%，相較傳統 Tesseract 引擎提升 40% 的端到端資訊抽取成功率。隨著大模型技術下放，OCR 已經從單純的「字元辨識」進化為「複雜版面理解 (Document Understanding)」。

👉 *延伸閱讀：[針對物件或場景影像進行分析與偵測 (觀念總結)](https://www.twman.org/AI/CV)* | *[12個流行的開源免費OCR項目](https://mp.weixin.qq.com/s/7EuhnQedAX6injBL_Dg_sQ)*

### 1. 基於視覺大模型 (VLM) 的高精度 OCR
處理手寫字跡、模糊掃描檔與不規則表單的最佳解法。

* **[Unlimited-OCR (無限 OCR)](https://github.com/baidu/Unlimited-OCR)** `[2026-06]` 🔥 `[長文件解析]` `[R-SWA注意力]` `[恆定顯存]` `[端到端SOTA]`
  * **核心優勢**：**打破長文件 OCR 記憶體暴增與降速死局，首創「恆定 KV Cache」的近無限解析黑科技！** 百度團隊針對傳統端到端大模型 (如 DeepSeek-OCR) 處理長文時效能斷崖式下跌的問題，受人類「邊看邊抄」的軟遺忘機制啟發，創新提出 R-SWA (參考滑動窗口注意力)。將解碼器切分為「全局可見的視覺參考段」與「固定寬度 (n=128) 的文字滑動窗口」。這讓模型在輸出超過 6000+ tokens 時，吞吐量依然穩如泰山 (7848 TPS)，並在 OmniDocBench v1.6 權威基準強勢奪下端到端 SOTA。
  * **解決痛點 / 推薦場景**：**完美解決了企業在進行「數十頁學術論文、厚重說明書、財務年報或書籍數位化」時，因顯存無限膨脹導致系統崩潰或推論極度緩慢的致命痛點。** 徹底終結過去必須「逐頁切分、反覆重置模型狀態」的工程補丁。極度適合用於**構建大模型 RAG 企業級巨型文檔清洗管線**、**自動化圖書掃描建檔**，以及對推論成本與 TPS 吞吐量要求極嚴苛的**高併發文檔解析雲端服務**。
  * **資源**：[🐙 GitHub 官方開源](https://github.com/baidu/Unlimited-OCR) | [📄 官方論文 (arXiv:2606.23050)](https://arxiv.org/abs/2606.23050)

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

* **[PP-OCRv6 (PaddleOCR 第六代)](https://github.com/PaddlePaddle/PaddleOCR)** `[2026-06]` 🔥
  * **核心優勢**：**1.5M 極限輕量至 34.5M 伺服器級全算力覆蓋，在結構化文字檢測與複雜場景精度上全面碾壓百億參數 VLM！** 首度推出 Tiny / Small / Medium 三檔模型，文字檢測與識別精度較前代呈現「代際躍升」（分別提升 4.9% 與 5.1%）。Medium 版本在 Intel Xeon CPU 結合 OpenVINO 最佳化下端到端推理僅需 1.4 秒（提速 5.2 倍），而 Tiny 版本在純前端瀏覽器單圖推理更可極限壓低至 97ms 級別。
  * **解決痛點 / 推薦場景**：**完美解決了大型多模態模型 (VLM) 推理昂貴、幻覺漏字，以及傳統 OCR 在「極端邊緣設備」與「特殊工業場景（如 PCB 電路板、數碼管、點陣字元、CAD 圖紙）」辨識率低落的致命痛點。** 面對複雜的繁體中文混排、古籍、模糊與傾斜文本也能展現極高魯棒性。是企業打造**高併發伺服器文檔解析**、**IoT 邊緣運算設備**與**純網頁端文字辨識 (Web OCR)** 的工業級開源霸主。

* **[PaddleOCR-VL-1.6 (生成式文件解析開源霸主)](https://github.com/PaddlePaddle/PaddleOCR)** `[2026-05-28]` 🔥
  * **核心優勢**：**打破傳統 OCR 僅能「認字」的極限，以 0.9B 極輕量 VLM 刷新 OmniDocBench 96.3% 新 SOTA，實現全頁面結構化解析！** 捨棄傳統切割拼湊，採用「版面分析 (Layout Analysis) ＋ 視覺語言模型 (VLM)」雙階段架構。不僅能精準捕捉文字，更能完美還原複雜表格、數學公式 (LaTeX)、圖表數據與生僻古籍，並直接輸出高質量的結構化 Markdown 或 JSON，且完全相容舊版架構實現零成本替換。
  * **解決痛點 / 推薦場景**：**完美解決了企業在建置 RAG 知識庫時，面對「掃描檔、雙欄合約、財報圖表導致語意斷裂與表格錯亂」的致命痛點。** 由於其極低的硬體門檻與強大的離線解析能力，極度推薦用於打造**企業級私有化 RAG 前處理管線**、**內網機密合約自動化審查**，以及**無網環境的高併發文檔數位化產線**，是資料不出門的最高 CP 值首選。
  * **資源**：[🐙 官方 GitHub](https://github.com/PaddlePaddle/PaddleOCR) | [🤗 模型權重 (HF)](https://huggingface.co/PaddlePaddle/PaddleOCR-VL-1.6) | [📦 一鍵本地 WebUI 部署](https://github.com/CHEN010325/paddleocr-vl-local)
  <br>`[RAG前處理]` `[完全離線部署]` `[版面分析]` `[開源霸主]`

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

> **擴散模型將生成式影像的控制精度提升至像素級別。** 透過 ControlNet 條件注入，Stable Diffusion 3 可以在 20 步內生成符合特定骨架或深度的 4K 圖像，將電商與遊戲資產的設計週期從數週壓縮至 3 小時內。擴散模型已經從單純的「文字生圖」，進化到「長影片生成」、「精準控制」與「一體化生成」。以下精選 2025-2026 年最具影響力的開源專案：

### 1. 影片生成大模型 (Video Generation)
突破硬體極限與時長限制，帶來電影級的視覺理解。

* **[SANA (NVIDIA 全端高效擴散生成生態系)](https://github.com/NVlabs/Sana)** `[2026-05]` 🔥
  * **核心優勢**：**徹底終結擴散模型算力霸權，以「線性注意力」與「32倍極致壓縮 (DC-AE)」重塑文生圖與世界模型的開源神作！** NVIDIA 聯合 MIT 與清華團隊重磅開源的 Apache 2.0 工具鏈。其基礎版僅需 0.6B 參數即可在不到 1 秒內產出極高畫質圖像，吞吐速度強勢輾壓 12B 的 Flux 達百倍；最新的 SANA-WM (世界模型) 更突破性地支援 720p、長達 1 分鐘且具備 6-DoF 相機精準控制的影片生成。全系列模型均可在 8GB~16GB 消費級顯卡上流暢運行。
  * **解決痛點 / 推薦場景**：**完美解決了傳統 DiT 模型「解析度/影片長度增加導致顯存 O(N²) 暴力膨脹」，以及「強化學習對齊訓練成本過高」的致命痛點。** 提供涵蓋極速 0.1 秒推理 (SANA-Sprint)、長影片生成 (LongSANA) 到低精度強化學習後訓練 (Sol-RL) 的全棧工具。極度推薦企業用於打造**即時互動設計畫布 (Real-time Canvas)**、**具身智能 (Embodied AI) 虛擬模擬環境**，以及需要極低算力門檻的**邊緣運算 (Edge AI) 視覺生成服務**。
  * **資源**：[🐙 GitHub 官方開源](https://github.com/NVlabs/Sana) | [🌐 官方線上 Demo](https://nv-sana.mit.edu/) | [🤗 Hugging Face 模型集](https://huggingface.co/collections/Efficient-Large-Model/sana)
  <br>`[線性擴散模型]` `[世界模型]` `[極低顯存門檻]` `[實時影片生成]`

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

* **[SceneScribe-1M (百萬級 3D 幾何與語意真實影片資料庫)](https://arxiv.org/abs/2604.07990)** `[2026-04]` 🔥
  * **核心優勢**：**打破 3D 幾何感知與影片生成的資料壁壘，首創全面自帶「連續深度圖、精準相機位姿、3D 點軌跡與結構化語意描述」的百萬級真實動態影片彈藥庫！** 憑藉強大的多模態自動標註管線與「語意＋幾何」雙軸篩選機制，一舉統整了感知與生成任務的底層數據需求，規模高達 1.56 億幀。
  * **解決痛點 / 推薦場景**：**完美解決了傳統影片生成模型「缺乏實體幾何常識（只能文生片，無法控制運鏡與物理空間）」以及 3D 感知模型「極度缺乏真實世界動態場景數據」的致命痛點。** 極度推薦給致力於打造**世界基礎模型 (World Foundation Model)**、**可控影片生成 (相機/深度條件引導 T2V)**、以及**自動駕駛與空間計算 4D 場景重建**的頂尖 AI 研發團隊，是邁向真實物理世界模擬器的必備底層資源。
  * **資源**：[🤗 Hugging Face 資料集](https://huggingface.co/datasets/wangyunnan/SceneScribe-1M) | [📄 論文](https://arxiv.org/abs/2604.07990)
  <br>`[世界基礎模型]` `[可控影片生成]` `[4D場景重建]` `[超大真實數據]`

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

> **神經輻射場 (NeRF) 與 3D Gaussian Splatting 加速了即時擬真分身的商用普及。** 採用單張照片驅動的 3D 虛擬人，能在 RTX 4090 上實現 4K 解析度 60 FPS 即時渲染，口型同步延遲低於 50ms，適用於全天候智能客服。虛擬數字人技術結合了語音驅動 (Audio-Driven)、唇形對齊 (Lip-Sync) 與 3D 渲染，是目前 AI 客服與虛擬直播的技術核心。

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

* **[Duix Avatar (全離線 AI 數位分身框架)](https://github.com/duixcom/Duix-Avatar)** `[持續更新]` 🔥
  * **核心優勢**：**打破虛擬人必須依賴雲端 API 的隱私痛點，實現「零資料外洩」的全離線影音同步黑科技！** 深度整合 ASR、TTS 與 CV 高精度唇動捕捉技術，只需極少樣本即可精準克隆個人的外貌輪廓與聲音特質。其最大的亮點在於本地端極致流暢的「唇形對位 (Lip-sync)」與表情連動，徹底擺脫傳統套殼工具的 PPT 配音生硬感。
  * **解決痛點 / 推薦場景**：**完美解決了企業與知識型創作者「不想頻繁真人出鏡，又擔心機密資料或臉部生物特徵上傳雲端遭濫用」的致命痛點。** 支援 8 國語言腳本生成，極度推薦給擁有獨立硬體（建議配備 RTX 4070 顯示卡、32GB 記憶體）的開發者與影音團隊，用來打造**企業內部多語培訓教材、本地閉環自動化短影音產線**，或是**無代碼/低代碼的個人專屬虛擬主播**。
  * **資源**：[🐙 GitHub](https://github.com/duixcom/Duix-Avatar) | [🌐 官方網站](https://www.duix.com) 
  <br>`[完全離線部署]` `[數位分身]` `[高精度唇形同步]` `[免上雲護隱私]`

* **[SoulX-LiveAct](https://github.com/Soul-AILab/SoulX-LiveAct)** `[2026-03-16]` 🔥
  * **核心優勢**：**首款突破「小時級」穩定生成的實時數字人框架，低延遲且具備極致性價比。** 來自 Soul App AI Lab，首創 Neighbor Forcing 與 ConvKV Memory 技術，解決了 AR 擴散模型在流式生成中常見的身份漂移與顯存爆量問題。在 H100 達成 20 FPS、0.94s 延遲，甚至支援在 RTX 5090 等消費級顯卡上流暢運行。
  * **解決痛點 / 推薦場景**：**徹底解決長時直播中常見的「人物變形」與「顯存線性增長」瓶頸。** 提供高精準度的口型同步 (Sync-C: 9.40) 與動作/表情 JSON 精細控制。是打造 24 小時不斷線直播、實時視訊通話（FaceTime 級體驗）與企業級虛擬客服的技術天花板方案。
  * **資源**：[🐙 GitHub](https://github.com/Soul-AILab/SoulX-LiveAct)

* **[StreamAvatar](https://streamavatar.github.io)** `[2025-12]` 🔥
  * **核心優勢**：**打破高質量、實時性與強交互的「不可能三角」，首創具備「聆聽反應」的流式擴散數字人！** 由清華、人大與騰訊混元聯合發表。透過創新的自回歸蒸餾（Auto-regressive Distillation），將傳統笨重的雙向 DiT 模型轉化為僅需 3 步去噪的因果生成器。在雙 H800 GPU 環境下，達成 1.20 秒超低延遲與 RTF < 1 的完美實時串流生成。
  * **解決痛點 / 推薦場景**：**徹底解決傳統擴散模型「無法即時串流」、「長時生成身份漂移」以及「只會說不會聽」的三大致命傷。** 獨創 Reference Sink 機制確保長影片不變形，並導入音訊交互注意力模組，讓數字人在用戶說話時能給出點頭、微笑等極度自然的「聽覺反饋」。是打造次世代雙向視訊客服、高保真 AI 實況主與沉浸式虛擬陪伴的巔峰架構。
  * **資源**：[🌐 官方專案主頁與 Demo](https://streamavatar.github.io) | [📄 論文](https://arxiv.org/abs/2512.22065)

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


## ❓ 電腦視覺開發常見問題解答 (FAQ)

**Q1: 工業 AOI 瑕疵樣本太少怎麼辦？**
A: 採用基於 PatchCore 的無監督異常檢測方案，僅需約 50-100 張「正常樣本」即可建立基準，檢出率可達 98% 以上。

**Q2: 邊緣運算 (Edge AI) 該選哪個物體偵測模型？**
A: 首選 YOLOv11 或 YOLO-NAS。在 Jetson Nano 級別設備上，INT8 量化後可維持 30 FPS 以上的即時偵測效能。

**Q3: 如何快速標註大量圖像分割資料集？**
A: 導入 SAM (Segment Anything) 作為輔助工具，點擊目標即可自動生成邊界，實測可節省 85% 以上的人工框選時間。

**Q4: 傳統 OCR 無法處理複雜表格怎麼解？**
A: 改用多模態大模型 (如 MinerU 或 DeepSeek-VL) 進行端到端解析，版面分析與文字提取的綜合準確率可提升至 96%。

**Q5: 虛擬數字人 (Digital Human) 的口型延遲可以多低？**
A: 結合最新的 3D Gaussian Splatting 與輕量化語音驅動模型，端到端的口型同步延遲已可穩定控制在 50ms 以內。

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