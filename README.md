{% include header.html %}

# 👁️ 電腦視覺 (CV) 與生成式影像・2026 資源全手冊

> **編者按：** 本頁面即時彙整 2026 年全球最尖端的電腦視覺技術。從定義行業標準的 **YOLO 家族**、**工業異常檢測 (AOI)**，到引爆創作革命的 **Flux 擴散模型** 與 **AI 影片生成**。
>
> 🚀 **核心收錄：** 涵蓋 2016 至今的視覺技術演進，包含目標偵測、圖像分割 (SAM 2/3)、OCR 文檔理解及最新的虛擬數位人技術。
>
> 歡迎訪問 **GitHub Repository**：
> 👉 [**GitHub: Computer-Vision-Paper**](https://github.com/Deep-Learning-101/Computer-Vision-Paper) (歡迎 Star ⭐)

---

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
**Anomaly Detection，異常檢測**

- 2026-01-29｜**LLM2CLIP**
  - 說明：結合大語言模型 (LLM) 強大的常識推理能力來增強 CLIP 模型的視覺表徵。解決了傳統 CLIP 在遇到罕見工業瑕疵或長尾分佈數據時容易誤判的問題，非常適合用於高精度的工業自動化光學檢測 (AOI) 與未見過異常的零樣本瑕疵檢測。
  - 資源：[📄 AlphaXiv](https://www.alphaxiv.org/abs/2411.04997) | [🐙 GitHub](https://microsoft.github.io/LLM2CLIP/) | [📝 公眾號解讀](https://mp.weixin.qq.com/s/-U03e1KZmFCoXTGzdYbC0Q)

- 2025-09-24｜**FS-SAM2**
  - 說明：Adapting Segment Anything Model 2 for Few-Shot Semantic Segmentation
  - 資源：[📄 AlphaXiv](https://www.alphaxiv.org/overview/2509.12105v1) | [📝 中文解讀：效能與效率雙優](https://zread.ai/fornib/FS-SAM2)

- 2025-09-20｜**MOCHA**
  - 說明：Multi-modal Objects-aware Cross-arcHitecture Alignment
  - 資源：[📄 AlphaXiv](https://www.alphaxiv.org/zh/overview/2509.14001v1) | [📝 中文解讀：注入 YOLO 性能大漲](https://zhuanlan.zhihu.com/p/1952054591035281418)

- 2025-07-16｜**CostFilter-AD**
  - 說明：Enhancing Anomaly Detection through Matching Cost Filtering
  - 資源：[🐙 GitHub](https://github.com/ZHE-SAPI/CostFilter-AD) | [📝 中文解讀：刷新無監督上限](https://zhuanlan.zhihu.com/p/1928870223529882075)

- 2025-06-13｜**One-to-Normal**
  - 說明：Anomaly Personalization (少樣本異常識別新突破)
  - 資源：[📄 AlphaXiv](https://www.alphaxiv.org/abs/2502.01201) | [📝 中文解讀](https://zhuanlan.zhihu.com/p/1916799842879018831)

- 2025-06-06｜**DualAnoDiff (CVPR 2025)**
  - 說明：Dual-Interrelated Diffusion Model for Few-Shot Anomaly Image Generation
  - 資源：[📄 AlphaXiv](https://www.alphaxiv.org/abs/2408.13509v3) | [📝 中文解讀：復旦騰訊優圖入選](https://www.qbitai.com/2025/06/291359.html)

- 2025-05-15｜**AdaptCLIP**
  - 說明：Adapting CLIP for Universal Visual Anomaly Detection
  - 資源：[📄 AlphaXiv](https://www.alphaxiv.org/overview/2407.15795) | [🐙 GitHub](https://github.com/aiiu-lab/AdaptCLIP) | [📝 中文解讀](https://mp.weixin.qq.com/s/w5x6T18aSZt9jxqMIdf-Yg)

- 2025-05-05｜**Multi-Modal LLM for AD**
  - 說明：Detect, Classify, Act: Categorizing Industrial Anomalies
  - 資源：[📄 AlphaXiv](https://www.alphaxiv.org/zh/overview/2505.02626) | [📚 DeepWiki](https://deepwiki.com/Sassanmtr/VELM) | [💾 Dataset](https://www.mvtec.com/company/research/datasets/mvtec-ad)

- 2025-04-27｜**AnomalyCLIP**
  - 說明：Object-agnostic Prompt Learning for Zero-shot AD
  - 資源：[📄 AlphaXiv](https://www.alphaxiv.org/overview/2310.18961) | [📚 DeepWiki](https://deepwiki.com/zqhang/AnomalyCLIP)

- 2025-04-26｜**PaDim**
  - 說明：經典無監督異常檢測方法
  - 資源：[📄 AlphaXiv](https://www.alphaxiv.org/zh/overview/2011.08785) | [📚 DeepWiki](https://deepwiki.com/xiahaifeng1995/PaDiM-Anomaly-Detection-Localization-master)

- 2025-04-12｜**AA-CLIP**
  - 說明：Enhancing Zero-shot Anomaly Detection via Anomaly-Aware CLIP
  - 資源：[📄 AlphaXiv](https://www.alphaxiv.org/zh/overview/2503.06661) | [📚 DeepWiki](https://deepwiki.com/Mwxinnn/AA-CLIP)

- 2025-03-25｜**Dinomaly**
  - 說明：The Less Is More Philosophy in Multi-Class Unsupervised AD
  - 資源：[🐙 GitHub](https://github.com/guojiajeremy/Dinomaly) | [📝 中文解讀](https://zhuanlan.zhihu.com/p/1886364053259146390)

---

## ObjectDetection
**Object Detection (目標偵測)**

- 2025｜**MCL (AAAI 2025)**
  - 說明：專為無人機空拍圖與衛星遙感影像設計的半監督目標檢測框架。透過多線索一致性學習，只需極少量的標註資料，就能在超大解析度影像中精準框出微小的車輛、建築物或農作物病灶，大幅降低農業監測與國土巡檢的資料標註成本。
  - 資源：[📄 AlphaXiv](https://www.alphaxiv.org/abs/2407.05909) | [🐙 GitHub](https://github.com/facias914/sood-mcl) | [📝 中文解讀](https://zhuanlan.zhihu.com/p/26788012528)

- 2025-07-24｜**OV-DINO**
  - 說明：開源工業開放詞彙目標檢測
  - 資源：[🐙 GitHub](https://github.com/wanghao9610/OV-DINO) | [📝 中文解讀](https://mp.weixin.qq.com/s/gLAVYFAH_39gT4XC0zWN0A)

- 2025-06-18｜**CountVid**
  - 說明：突破傳統模型只能數「特定訓練類別」的限制，支援在動態影片中透過提示 (Prompt) 實現「指哪數哪」的開放世界物件計數。極度適合應用於智慧城市的交通車流監控、大型活動的人流密度預警，或是生產線上快速移動物件的良率計算。
  - 資源：[📄 AlphaXiv](https://www.alphaxiv.org/abs/2506.15368) | [📝 中文解讀](https://mp.weixin.qq.com/s/hICrrfEgriyktoIxnbjPEQ)

- 2025-06-15｜**GeoPix**
  - 說明：像素級遙感多模態大模型
  - 資源：[🐙 GitHub](https://github.com/Norman-Ou/GeoPix) | [📝 北大實驗室介紹](https://3slab.pku.edu.cn/info/1026/2121.htm)

- 2025-05-23｜**VisionReasoner**
  - 說明：用強化學習統一視覺感知與推理 (對標 Qwen2.5-VL)
  - 資源：[🐙 GitHub](https://github.com/dvlab-research/VisionReasoner) | [📝 中文解讀](https://mp.weixin.qq.com/s/vECz3i_-dzvlDr3BdRLPWQ)

- 2025-03-14｜**Falcon**
  - 說明：A Remote Sensing Vision-Language Foundation Model
  - 資源：[📄 AlphaXiv](https://www.alphaxiv.org/abs/2503.11070) | [📚 DeepWiki](https://deepwiki.com/TianHuiLab/Falcon)

---

## Segmentation
**Segmentation (圖像分割)**

- **SAM 3**
  - 資源：[🐙 GitHub](https://github.com/facebookresearch/sam3) | [📝 公眾號解讀](https://mp.weixin.qq.com/s/7uDHXQd1ES2mV4dZFB7VMw)

- **Perceive Anything Model**
  - 說明：Recognize, Explain, Caption, and Segment Anything (對標 SAM2 + LLM)
  - 資源：[📄 AlphaXiv](https://www.alphaxiv.org/zh/overview/2506.05302v1) | [📝 中文解讀](https://zhuanlan.zhihu.com/p/1919709726209446971)

- **RemoteSAM**
  - 說明：Towards Segment Anything for Earth Observation
  - 資源：[📄 AlphaXiv](https://www.alphaxiv.org/abs/2505.18022v3) | [📚 DeepWiki](https://deepwiki.com/1e12Leon/RemoteSAM)

- **InstructSAM**
  - 說明：專為地球觀測 (Earth Observation) 打造的免訓練 (Training-Free) 圖像分割框架。使用者只需輸入自然語言指令（例如「框出所有的太陽能板」或「標記森林大火區域」），模型就能自動完成精準的地理圖資分割，是災防應變與都市 GIS 規劃的強大輔助工具。
  - 資源：[🌐 Project](https://voyagerxvoyagerx.github.io/InstructSAM/) | [📄 AlphaXiv](https://www.alphaxiv.org/zh/overview/2505.15818v1) | [📚 DeepWiki](https://deepwiki.com/VoyagerXvoyagerx/InstructSAM)

- **SAM 2 & Variants** (SAM 2 相關變體)
  - [**Meta SAM 2**](https://ai.meta.com/sam2/): Meta 官方最新分割一切模型。
    - [📝 60行程式碼微調 SAM 2](https://mp.weixin.qq.com/s/YfgYCzvi0cXxOFIfQvE_9w)
  - [**Grounded SAM 2**](https://github.com/IDEA-Research/Grounded-SAM-2): Ground and Track Anything in Videos.
  - [**SAM2Long**](https://github.com/Mark12Ding/SAM2Long): Meta 官方的 SAM 2 在面對超過數分鐘的影片時容易丟失目標。此變體透過長效記憶體機制強化了追蹤穩定度，是影視後期特效「自動摳圖 (Rotoscoping)」的開源利器。
  - [**SAM2-Adapter**](https://github.com/tianrun-chen/SAM-Adapter-PyTorch): 首次讓 SAM 2 適應下游任務。
  - [**SAM2Point**](https://github.com/ZiyuGuo99/SAM2Point): 將 SAM 2 的分割能力從 2D 圖片延伸至 3D 點雲 (Point Cloud) 數據。為自駕車的光達 (LiDAR) 感測分析與 3D 醫學影像（如 MRI/CT）分割帶來了革命性的零樣本 (Zero-shot) 處理能力。

- **Other Notable Models**
  - [**SAMURAI**](https://yangchris11.github.io/samurai/): KF + SAM2 解決快速移動或自遮擋問題。
  - [**MatAnyone**](https://github.com/pq-yang/MatAnyone): 視訊摳圖，髮絲級還原。
  - [**Exact (CVPR 2025)**](https://github.com/MiSsU-HH/Exact): 遙感影像時間序列弱監督學習。
  - [**SegAnyMo (CVPR 2025)**](https://github.com/nnanhuang/SegAnyMo): Segment Any Motion in Videos.

---

## OCR
**Optical Character Recognition (光學文字識別)**
**[針對物件或場景影像進行分析與偵測](https://www.twman.org/AI/CV)**

- [使用開源模型強化您的 OCR 工作流程](https://huggingface.co/blog/zh/ocr-open-models)
- [12個流行的開源免費OCR項目](https://mp.weixin.qq.com/s/7EuhnQedAX6injBL_Dg_sQ)

- 2026-01-28 | **OpenDoc-0.1B**
  - 資源：[🐙 GitHub](https://github.com/Topdu/OpenOCR) | [📝 公眾號解讀](https://mp.weixin.qq.com/s/TJdTLNBSgHy-3I1o98OEAQ) | [📝 公眾號解讀](https://mp.weixin.qq.com/s/2a8LruNJvHCxcuPslp0Z1Q)

- 2026-01-27 | **DeepSeek-OCR 2**
  - 說明：DeepSeek 團隊開源的新一代視覺語言模型，專精於複雜場景的高精度文字辨識。能完美應對手寫字跡、模糊掃描檔、多語系混合以及發票收據等不規則排版，是企業打造自動化財務報帳系統、或是大量紙本表單數位化的高性價比底座。
  - 資源：[🐙 GitHub](https://github.com/deepseek-ai/DeepSeek-OCR-2/) | [🤗 HuggingFace](https://huggingface.co/deepseek-ai/DeepSeek-OCR-2) | [📝 公眾號解讀](https://mp.weixin.qq.com/s/DOm_hg6DWA_OjcsLuUQ9Hw)

- 2025-11-30｜**HunyuanOCR**
  - 資源：[🐙 GitHub](https://github.com/Tencent-Hunyuan/HunyuanOCR) | [📝 騰訊混元 1B 級全能模型](https://zhuanlan.zhihu.com/p/1977498008712131326)

- 2025-10-21 | **Chandra OCR**
  - 資源：[🐙 GitHub](https://github.com/datalab-to/chandra) | [📝 超越DeepSeek-OCR！ OCR領域的革命性突破：Chandra OCR本地部署+真實評測](https://zhuanlan.zhihu.com/p/1969019468937144099)

- 2025-10-19｜**PaddleOCR-VL**
  - 資源：[🤗 HuggingFace](https://huggingface.co/PaddlePaddle/PaddleOCR-VL) | [📝 圖片辨識轉文字巔峰之作](https://zhuanlan.zhihu.com/p/1964600336103745187)

- 2025-08-18｜**DianJin-OCR-R1**
  - 資源：[🐙 GitHub](https://github.com/aliyun/qwen-dianjin) | [📝 點金 OCR-R1：模糊蓋章、跨頁表格全拿下](https://mp.weixin.qq.com/s/cOo0sqwDt3ARid70wBaYVA)

- 2025-07-30｜**dots.ocr**
  - 資源：[🤗 HuggingFace](https://huggingface.co/rednote-hilab/dots.ocr) | [📝 本地部署 1.7B 超強 OCR](https://zhuanlan.zhihu.com/p/1935120171573413613)

- 2025-06-16｜**OCRFlux**
  - 說明：專治各種「反人類排版」的 PDF 解析救星！結合大語言模型 (LLM) 強大的上下文理解能力，能精準還原雙欄排版、跨頁表格與複雜的 ESG 財報數據。極度適合用來建立企業私有知識庫，或是作為 RAG (檢索增強生成) 系統的前端資料清洗管線。
  - 資源：[🐙 GitHub](https://github.com/chatdoc-com/OCRFlux) | [🌐 Demo](https://ocrflux.pdfparser.io/#/)

- 2025-06-05｜**MonkeyOCR**
  - 資源：[📚 DeepWiki](https://deepwiki.com/Yuliang-Liu/MonkeyOCR) | [📄 AlphaXiv](https://www.alphaxiv.org/overview/2506.05218)

  - 2025-03-05｜**OpenOCR**
  - 資源：[🐙 GitHub](https://github.com/Topdu/OpenOCR) | [📝 通用OCR工具OpenOCR開源
](https://zhuanlan.zhihu.com/p/10259507246)

- 2025-03-05｜**PP-DocBee**
  - 資源：[🐙 GitHub](https://github.com/PaddlePaddle/PaddleMIX/tree/develop/deploy/ppdocbee) | [📝 百度文檔影像理解](https://zhuanlan.zhihu.com/p/28715553656)

- 2025-03-03｜**olmocr**
  - 資源：[🐙 GitHub](https://github.com/allenai/olmocr) | [📝 本地部署精準提取 PDF](https://www.aivi.fyi/llms/deploy-olmOCR)

- 2025-02-05｜**MinerU**
  - 說明：將 PDF 與網頁完美轉換為乾淨 Markdown 格式的開源神器。不僅能精準提取內文，連學術論文中的數學公式、程式碼區塊與圖表都能高保真還原，是開發者在準備大語言模型 (LLM) 預訓練語料或微調 (Fine-tuning) 數據時不可或缺的高效清洗工具。
  - 資源：[🐙 GitHub](https://github.com/opendatalab/MinerU) | [📝 PDF 轉 Markdown 神器](https://mp.weixin.qq.com/s/ci5wp6gICTCtaRZfn5yWUQ)

- 2024-12-15｜**markitdown**
  - 資源：[🐙 GitHub](https://github.com/microsoft/markitdown)

- 2024-10-29｜**OmniParser**
  - 資源：[🐙 GitHub](https://github.com/AlibabaResearch/AdvancedLiterateMachinery/tree/main/OCR/OmniParser) | [📝 Alibaba 出品：通用文檔複雜場景抽取](https://mp.weixin.qq.com/s/_1Aatpna7poIVRhfYk4aAQ)

- 2024-09-11｜**GOT-OCR-2.0**
  - 資源：[📝 模型開源介紹](https://mp.weixin.qq.com/s/rQL-Q0TGhT6e8Ti4zZalrg) | [📝 OCR 2.0 時代來了](https://mp.weixin.qq.com/s/W-Ult-F3pU6Wvx3fHEN8yA)

- 2024-08-20｜**PDF 轉 MarkDown 工具**
  - 資源：[📝 萬物皆可 AI 化！12000 人圍觀的開源工具](https://www.53ai.com/news/MultimodalLargeModel/2024082059736.html)

- **其他實用工具與資源**
  - **RapidOCR**：[🐙 GitHub](https://github.com/RapidAI/RapidOCR/blob/main/docs/README_zh.md)
  - **TableStructureRec**：[🐙 GitHub](https://github.com/RapidAI/TableStructureRec) | [📝 表格結構辨識推理庫](https://zhuanlan.zhihu.com/p/668484933)
  - **PaddleOCR 教學**：[📝 用 PPOCRLabel 微調醫療診斷書和收據](https://blog.twman.org/2023/07/wsl.html)

---


## Diffusion Model
**Diffusion Model (擴散模型)**


- 2025-05-28｜**Jodi**
  - 說明：視覺理解 & 生成大一統模型
  - 資源：[📄 AlphaXiv](https://www.alphaxiv.org/zh/overview/2505.19084) | [🌐 Project](https://vipl-genun.github.io/Project-Jodi/)

- 2025-05-27｜**AnomalyAny (CVPR 2025)**
  - 說明：Stable Diffusion 協助視覺異常檢測，無需訓練
  - 資源：[🌐 Project](https://hansunhayden.github.io/AnomalyAny.github.io/) | [📝 中文解讀](https://zhuanlan.zhihu.com/p/1910284073231942689)

- 2025-05-23｜**HivisionIDPhotos**
  - 說明：智慧證件照生成神器 (摳圖、換背景、任意尺寸)
  - 資源：[📚 DeepWiki](https://deepwiki.com/Zeyi-Lin/HivisionIDPhotos) | [📝 教學文章](https://zhuanlan.zhihu.com/p/718725351)

- 2025-05-19｜**Index-AniSora**
  - 說明：B 站開源 SOTA 動畫影片生成模型
  - 資源：[📄 AlphaXiv](https://www.alphaxiv.org/overview/2504.10044) | [📚 DeepWiki](https://deepwiki.com/bilibili/Index-anisora) | [📝 中文解讀](https://zhuanlan.zhihu.com/p/1908150671540224717)

- 2025-04-26｜**Insert Anything**
  - 資源：[📄 AlphaXiv](https://www.alphaxiv.org/zh/overview/2504.15009) | [📚 DeepWiki](https://deepwiki.com/song-wensong/insert-anything)

- 2025-04-24｜**Phantom**
  - 說明：字節跳動 1280x720 影片生成模型，10G 顯存可用
  - 資源：[🐙 GitHub](https://github.com/Phantom-video/Phantom) | [📝 實測報告](https://zhuanlan.zhihu.com/p/1898688574477545694)

- 2025-04-22｜**MAGI-1**
  - 說明：Sand AI 全球首個自回歸影片生成大模型
  - 資源：[🐙 GitHub](https://github.com/SandAI-org/Magi-1) | [📝 性能亮點解析](https://www.zhihu.com/question/1898030232184795448)

- 2025-04-22｜**SkyReels V2**
  - 說明：全球首個無限時長影片生成，電影級理解
  - 資源：[🐙 GitHub](https://github.com/SkyworkAI/SkyReels-V2) | [📝 媒體報導](https://www.qbitai.com/2025/04/275531.html)

- 2025-04-14｜**FramePack**
  - 說明：ComfyUI 插件，6G 顯存跑 13B 模型，支援 1 分鐘影片
  - 資源：[🐙 GitHub](https://github.com/kijai/ComfyUI-FramePackWrapper) | [📝 性價比分析](https://zhuanlan.zhihu.com/p/1896487969470251546)

- 2025-04-14｜**Fantasy-talking**
  - 說明：基於 Wan2.1 的音訊驅動數字人
  - 資源：[🌐 Project](https://fantasy-amap.github.io/fantasy-talking/) | [📝 解讀文章](https://zhuanlan.zhihu.com/p/1892895916354148118)

- 2025-04-05｜**SkyReels-A2**
  - 資源：[📄 AlphaXiv](https://www.alphaxiv.org/zh/overview/2504.02436) | [📚 DeepWiki](https://deepwiki.com/SkyworkAI/SkyReels-A2) | [📝 中文解讀](https://zhuanlan.zhihu.com/p/1892709305301590652)

- 2025-03-10｜**HunyuanVideo-I2V**
  - 說明：騰訊開源圖生視訊模型 + LoRA 訓練腳本
  - 資源：[🐙 GitHub](https://github.com/Tencent/HunyuanVideo-I2V) | [📝 實戰教學](https://zhuanlan.zhihu.com/p/29110060025)

- 2025-02-25｜**Wan-Video**
  - 說明：阿里萬相大模型開源，全模態、全尺寸
  - 資源：[🐙 GitHub](https://github.com/Wan-Video/Wan2.1) | [📝 媒體報導](https://finance.sina.com.cn/jjxw/2025-02-26/doc-inemukxr9127437.shtml)

- 2025-02-14｜**FlashVideo**
  - 說明：字節跳動視訊增強演算法，102 秒生成 1080P 影片
  - 資源：[🐙 GitHub](https://github.com/FoundationVision/FlashVideo) | [📝 解讀文章](https://zhuanlan.zhihu.com/p/23702953115)

- 2025-01-28｜**Sana (ICLR 2025 Oral)**
  - 說明：英偉達/MIT/清華開源，比 FLUX 快 100 倍
  - 資源：[🐙 GitHub](https://github.com/NVlabs/Sana) | [📝 中文解讀](https://zhuanlan.zhihu.com/p/19489214543)

- **Flux & Ecosystem**
  - **Flux Models**: [🤗 Black Forest Labs](https://huggingface.co/black-forest-labs)
    - [Canny-dev](https://huggingface.co/spaces/black-forest-labs/FLUX.1-Canny-dev) | [Depth-dev](https://huggingface.co/spaces/black-forest-labs/FLUX.1-Depth-dev) | [Fill-dev](https://huggingface.co/spaces/black-forest-labs/FLUX.1-Fill-dev) | [Redux-dev](https://huggingface.co/spaces/black-forest-labs/FLUX.1-Redux-dev)
  - **PuLID (2024-11-29)**: [🐙 GitHub](https://github.com/ToTheBeginning/PuLID) | [📝 ComfyUI 教學](https://mp.weixin.qq.com/s/07BMFHaSasl7-PFtkN6_Zg)
  - **Leffa (2024-12-17)**: [🐙 GitHub](https://github.com/franciszzj/Leffa) | [📝 Meta AI 人物特徵保持](https://juejin.cn/post/7449325873725276196)
  - **MagicQuill (2024-11-26)**: [🐙 GitHub](https://github.com/magic-quill/MagicQuill) | [🤗 Space](https://huggingface.co/spaces/AI4Editing/MagicQuill) | [📝 AI P 圖神器](https://mp.weixin.qq.com/s/Pc3xRP8_9BxkVSRNznkplw)

- **Practical Tools (ComfyUI & Others)**
  - **OOTDiffusion**: [🐙 GitHub](https://github.com/levihsu/OOTDiffusion) | [📝 AI 換裝神器](https://mp.weixin.qq.com/s/B2rNCjJLo8coYzoHGPnVaw)
  - **ComfyUI Impact Pack**: [🐙 GitHub](https://github.com/ltdrdata/ComfyUI-Impact-Pack) | [📝 最強臉部修復](https://mp.weixin.qq.com/s/hNQ9BfdGbRQ_Osus-yMJWg)
  - **OmniGen**: [🐙 GitHub](https://github.com/AIFSH/OmniGen-ComfyUI) | [📝 全能影像生成](https://mp.weixin.qq.com/s/msGK0FmNs3T3jbUBHfR9DA)

---

## Digital Human
**Digital Human (虛擬數字人)**

- **SoulX-FlashTalk**
  - 資源：[📝 GitHub ](https://github.com/Soul-AILab/SoulX-FlashTalk) | [📝 公眾號解讀](https://mp.weixin.qq.com/s/eArkEQco000XbA3-vGwwRw)

- **FlowAct-R1**
  - 資源：[📝 GitHub ](https://grisoon.github.io/FlowAct-R1/) | [📝 公眾號解讀](https://mp.weixin.qq.com/s/VOBYaVpOAC3AgJWKZN1tKA)

- **EchoMimic V3**
  - 資源：[📝 GitHub ](https://github.com/antgroup/echomimic_v3) | [📝 公眾號解讀](https://mp.weixin.qq.com/s/cHL-ROirvxLxJNtabke0Fg)

- **PersonaLive**
  - 資源：[📝 GitHub ](https://github.com/GVCLab/PersonaLive) | [📝 公眾號解讀](https://mp.weixin.qq.com/s/R5OXddOHsCYoGRoFJeFrZA)

- **Open Avatar Chat**
  - 資源：[📝 專案介紹](https://zread.ai/HumanAIGC-Engineering/OpenAvatarChat) | [📝 GitHub 爆火神器，本地部署無套路](https://mp.weixin.qq.com/s/eNRbU4lZLgdpe_iNSNcfGA)

- **HeyGem**
  - 資源：[🐙 GitHub](https://github.com/GuijiAI/HeyGem.ai) | [📝 數字人克隆神器](https://zhuanlan.zhihu.com/p/29274862393)

- **Duix**
  - 資源：[🐙 GitHub](https://github.com/GuijiAI/duix.ai) | [📝 全球首個真人數字人開源](https://zhuanlan.zhihu.com/p/716583514)

- **Linly-Talker**
  - 說明：結合 LLM 與視覺模型的智能交互系統
  - 資源：[🐙 GitHub](https://github.com/Kedreamix/Linly-Talker)

- **CVPR 2025 / NeurIPS Resources**
  - **EchoMimicV2 (CVPR 2025)**: [🐙 GitHub](https://github.com/antgroup/echomimic_v2) - Striking, Simplified Human Animation.
  - **Hallo3 (CVPR 2025)**: [🐙 GitHub](https://github.com/fudan-generative-vision/hallo3) - Highly Dynamic Portrait Animation.
  - **MimicTalk (NeurIPS 2024)**: [🐙 GitHub](https://github.com/yerfor/MimicTalk) - 3D talking face.

- **Other Tools**
  - **JoyGen**: [🐙 GitHub](https://github.com/JOY-MM/JoyGen) (Audio-Driven 3D Editing)
  - **Latentsync**: [🐙 GitHub](https://github.com/bytedance/LatentSync)
  - **MuseTalk**: [🐙 GitHub](https://github.com/TMElyralab/MuseTalk)

---

## Image Recognition
**Image Recognition (圖像識別)**


- **ViT (Vision Transformer)**
  - 資源：[🐙 GitHub](https://github.com/google-research/vision_transformer) | [📝 解析文章](https://zhuanlan.zhihu.com/p/445122996) | [📝 遷移表現分析](https://zhuanlan.zhihu.com/p/463608959)

- **Swin Transformer**
  - 資源：[🐙 GitHub](https://github.com/microsoft/Swin-Transformer) | [📝 用 CNN 方式打敗 CNN](https://zhuanlan.zhihu.com/p/362690149)

- **EfficientNetV2**
  - 資源：[🐙 GitHub](https://github.com/d-li14/efficientnetv2.pytorch) | [📝 更小更快的訓練](https://zhuanlan.zhihu.com/p/361873583)

---

## Document AI
**Document Understanding & OCR (文檔理解與文字識別)**

- **Donut (2022)**: OCR-free Document Understanding Transformer. [📄 arXiv:2111.15664](./donut.md)
- **LayoutParser (2021)**: Unified toolkit for Deep Learning Based Document Analysis. [📄 arXiv:2103.15348](./LayoutParser.md)
- **TrOCR (2021)**: Transformer-based OCR with Pre-trained Models. [📄 arXiv:2109.10282](./TrOCR.md)
- **DiT (2022)**: Self-supervised Pre-training for Document Image Transformer. [📄 arXiv:2203.02378](./DiT.md)
- **Nougat (2023)**: Neural Optical Understanding for Academic Documents. [📄 arXiv:2308.13418](https://facebookresearch.github.io/nougat/)

<details>
<summary><strong>📚 LayoutLM Series (點擊展開)</strong></summary>

- **LayoutLM (2020)**: Pre-training of Text and Layout. [📄 arXiv:1912.13318](./LayoutLM.md)
- **LayoutLMv2 (2021)**: Multi-modal Pre-training. [📄 arXiv:2012.14740](./LayoutLMv2.md)
- **LayoutXLM (2021)**: Multilingual Visually-rich Document Understanding. [📄 arXiv:2104.08836](./LayoutXLM.md)
- **LayoutLMv3 (2022)**: Pre-training with Unified Text and Image Masking. [📄 arXiv:2204.08387](./LayoutLMv3.md)
</details>

- **Scene Text Recognition**
  - **ABINet (2021)**: Read Like Humans. [📄 arXiv:2103.06495](./ABINet.md)
  - **ABINet++ (2022)**: Iterative Language Modeling for Text Spotting. [📄 arXiv:2211.10578](./ABINet%2B%2B.md)
  - **ABCNet v2 (2021)**: Adaptive Bezier-Curve Network. [📄 arXiv:2105.03620](./ABCNet_v2.md)
  - **SVTR (2022)**: Scene Text Recognition with a Single Visual Model. [📄 arXiv:2205.00159](./SVTR.md)

---

## DeepFake Detection
**DeepFake Detection (深度偽造偵測)**

- **Multi-attentional Deepfake Detection (CVPR 2021)**
  - H. Zhao et al., Proceedings of the IEEE/CVF CVPR 2021.

- **Geometric Features (CVPR 2021)**
  - Improving Efficiency and Robustness through Precise Geometric Features. Sun, Zekun et al.

- **3D Decomposition (CVPR 2021)**
  - Face Forgery Detection by 3D Decomposition. Xiangyu Zhu et al.


<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "TechArticle",
  "mainEntityOfPage": {
    "@type": "WebPage",
    "@id": "https://deep-learning-101.github.io/Computer-Vision"
  },
  "headline": "2026 電腦視覺 (CV) 全攻略：從 YOLOv11 目標偵測到 Flux/Wan-Video 影像生成",
  "description": "2026 年最強 CV 資源清單。收錄 YOLOv11/v10/v9、SAM 3 圖像分割、Flux.1 生圖、Wan-Video 影片生成、DeepSeek-OCR 2 及工業異常檢測 (Anomaly Detection) 與虛擬數位人技術。",
  "image": "https://raw.githubusercontent.com/Deep-Learning-101/.github/blob/main/images/DeepLearning101.JPG?raw=true",
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
      "url": "https://raw.githubusercontent.com/Deep-Learning-101/.github/blob/main/images/DeepLearning101.JPG?raw=true"
    }
  },
  "datePublished": "2026-03-29",
  "dateModified": "2026-03-29",
  "keywords": "電腦視覺, Computer Vision, YOLOv11, YOLOv9, Flux.1, Sana, Wan-Video, SAM 3, 異常檢測, Anomaly Detection, OCR, DeepSeek-OCR, 數位人, Digital Human, 影像生成, Diffusion Model, 遙感影像分析",
  "about": [
    {
      "@type": "Service",
      "name": "判別式視覺技術 (Object Detection, Segmentation, OCR)"
    },
    {
      "@type": "Service",
      "name": "生成式視覺技術 (Diffusion Models, Video Generation, Digital Human)"
    }
  ]
}
</script>  