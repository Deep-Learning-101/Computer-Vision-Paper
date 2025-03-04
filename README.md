#
https://www.twman.org/AI/CV

https://huggingface.co/DeepLearning101
#

<details open>
<summary><strong>手把手帶你一起踩AI坑：https://reurl.cc/g6GlZX</strong></summary>
   
- [白話文手把手帶你科普 GenAI](https://blog.twman.org/2024/08/LLM.html)
   
- [ComfyUI + Stable Diffuision](https://blog.twman.org/2024/11/diffusion.html)
  
- [大型語言模型直接就打完收工？](https://blog.twman.org/2024/09/LLM.html)
  
- [那些檢索增強生成要踩的坑](https://blog.twman.org/2024/07/RAG.html)
  
- [那些大型語言模型要踩的坑](https://blog.twman.org/2024/02/LLM.html)
  
- [Large Language Model，LLM](https://blog.twman.org/2023/04/GPT.html)
  
- [那些自然語言處理踩的坑](https://blog.twman.org/2021/04/NLP.html)

- [那些語音處理 (Speech Processing) 踩的坑](https://blog.twman.org/2021/04/ASR.html)

- [那些ASR和TTS可能會踩的坑](https://blog.twman.org/2024/02/asr-tts.html)
</details>

# Computer-Vision (電腦視覺)


## Segmentation (圖像分割)

- [Meta Segment Anything Model 2 (SAM 2)](https://ai.meta.com/sam2/)
   - [60行程式碼訓練/微調Segment Anything 2](https://mp.weixin.qq.com/s/YfgYCzvi0cXxOFIfQvE_9w)
   - [CLIPSeg：Image Segmentation Using Text and Image Prompts](https://github.com/timojl/clipseg)：[Huggingface Space](https://huggingface.co/spaces/taesiri/CLIPSeg)
      - [哥廷根大學提出CLIPSeg，能同時作三個分割任務的模型](https://mp.weixin.qq.com/s/evKssKulZiUssLN71t6_Lw)
      - [SAM與CLIP強強聯手，實現22000類的分割與識別](https://mp.weixin.qq.com/s/evKssKulZiUssLN71t6_Lw)
- [SAMURAI](https://yangchris11.github.io/samurai/)
   - [無需訓練或微調即可得到穩定、準確的追蹤效果！ KF + SAM2 解決快速移動或自遮擋的物件追蹤問題](https://mp.weixin.qq.com/s/iU3Bk_uO01GWUxAtIBsrWQ)
   - [經典卡爾曼濾波器改進影片版「分割一切」，網友：好優雅的方法](https://www.qbitai.com/2024/11/223020.html)
- [Grounded SAM 2: Ground and Track Anything in Videos](https://github.com/IDEA-Research/Grounded-SAM-2)
   - [Grounded-Segment-Anything](https://huggingface.co/spaces/yizhangliu/Grounded-Segment-Anything)
- [SAM2Long](https://github.com/Mark12Ding/SAM2Long)：[大幅提升SAM 2性能！港中文提出SAM2Long，複雜長視頻的分割模型](https://mp.weixin.qq.com/s/henvaxGoNgx24NLQV1Qj2w)
- [SAM2-Adapter](https://github.com/tianrun-chen/SAM-Adapter-PyTorch)：[SAM 2無法分割一切？ SAM2-Adapter：首次讓SAM 2在下游任務適應調校！](https://mp.weixin.qq.com/s/3z-LshKAgbSzNCzyoLOuag)
- [SAM2Point](https://github.com/ZiyuGuo99/SAM2Point)：[可提示3D 分割研究里程碑！ SAM2Point：SAM2加持可泛化任3D場景、任意提示！](https://mp.weixin.qq.com/s/TnTK5UE7O_hcrNzloxBmAw)



## Diffusion model (擴散模型)

- 2025-02-25：[Wan-Video](https://github.com/Wan-Video/Wan2.1)：[超越Sora！阿里萬相大模型正式開源！全模態、全尺寸大模型開源](https://finance.sina.com.cn/jjxw/2025-02-26/doc-inemukxr9127437.shtml)
- 2025-02-14：[FlashVideo](https://github.com/FoundationVision/FlashVideo)：[來自位元組的視訊增強全新開源演算法，102秒產生1080P視頻](https://zhuanlan.zhihu.com/p/23702953115)
- 2025-01-28：[Sana](https://github.com/NVlabs/Sana)：[ICLR 2025 Oral] Efficient High-Resolution Image Synthesis with Linear Diffusion Transformer；[比FLUX快100倍！英偉達聯手MIT、清華開源超快AI影像產生模型](https://zhuanlan.zhihu.com/p/19489214543)
- [Flux](https://huggingface.co/black-forest-labs)
   - [Flux.1-canny-dev](https://huggingface.co/spaces/black-forest-labs/FLUX.1-canny-dev)：[https://huggingface.co/black-forest-labs/FLUX.1-Canny-dev/](https://huggingface.co/black-forest-labs/FLUX.1-Canny-dev/)
   - [Flux.1-depth-dev](https://huggingface.co/spaces/black-forest-labs/FLUX.1-Depth-dev)：[https://huggingface.co/black-forest-labs/FLUX.1-Depth-dev/](https://huggingface.co/black-forest-labs/FLUX.1-Depth-dev/)
   - [Flux.1-fill-dev](https://huggingface.co/spaces/black-forest-labs/FLUX.1-Fill-dev)：[https://huggingface.co/black-forest-labs/FLUX.1-Fill-dev/](https://huggingface.co/black-forest-labs/FLUX.1-Fill-dev/)
   - [Flux.1-redux-dev](https://huggingface.co/spaces/black-forest-labs/FLUX.1-Redux-dev)：[https://huggingface.co/black-forest-labs/FLUX.1-Redux-dev/](https://huggingface.co/black-forest-labs/FLUX.1-Redux-dev/)
      - 2024-11-26：[Flux官方重繪+擴圖+風格參考+ControlNet](https://mp.weixin.qq.com/s/Kj1nyJNTpoZ94JjO4FMw_g)
      - 2024-11-25：[最新flux_fill_inpaint模型體驗。](https://mp.weixin.qq.com/s/OPknDJXH1_oezSR86c_png)
- 2024-12-17：[Leffa](https://github.com/franciszzj/Leffa)：[Leffa：Meta AI 開源精確控制人物外觀和姿勢的圖像生成框架，在生成穿著的同時保持人物特徵](https://juejin.cn/post/7449325873725276196)
- 2024-11-29：[PuLID, Pure and Lightning ID Customization via Contrastive Alignment](https://github.com/ToTheBeginning/PuLID)：[https://github.com/balazik/ComfyUI-PuLID-Flux](https://github.com/balazik/ComfyUI-PuLID-Flux)
   - 2024-11-07：[搞定ComfyUI-PuLID-Flux節點只要這幾步！附一鍵壓縮包](https://mp.weixin.qq.com/s/07BMFHaSasl7-PFtkN6_Zg)
   - 2024-10-08：[一文搞懂PuLID FLUX人物換臉&風格遷移](https://mp.weixin.qq.com/s/V-2Cp8_xFnHQNFn35aGdLg)
- 2024-11-26：[MagicQuill](https://github.com/magic-quill/MagicQuill)：[https://huggingface.co/spaces/AI4Editing/MagicQuill](https://huggingface.co/spaces/AI4Editing/MagicQuill)
   - [MagicQuill，登上Huggingface趨勢榜榜首的AI P圖神器](https://mp.weixin.qq.com/s/Pc3xRP8_9BxkVSRNznkplw)
- 2024-11-26：[OOTDiffusion](https://github.com/levihsu/OOTDiffusion)：[https://huggingface.co/spaces/levihsu/OOTDiffusion](https://huggingface.co/spaces/levihsu/OOTDiffusion)
   - [開源AI換裝神器OOTDiffusion](https://mp.weixin.qq.com/s/B2rNCjJLo8coYzoHGPnVaw)
- 2024-11-24：[Comfyui Impact Pack](https://github.com/ltdrdata/ComfyUI-Impact-Pack)
   - [Comfyui 最強臉部修復工具Impact Pack](https://mp.weixin.qq.com/s/hNQ9BfdGbRQ_Osus-yMJWg)
- 2024-11-05：[ComfyUI OmniGen @ 北京人工智慧研究院](https://github.com/AIFSH/OmniGen-ComfyUI)：[https://huggingface.co/spaces/Shitao/OmniGen](https://huggingface.co/spaces/Shitao/OmniGen)
   - [ComfyUI 影像生成模型OmniGen，人物一致性處理的也太好了](https://mp.weixin.qq.com/s/msGK0FmNs3T3jbUBHfR9DA)
   - [全能影像生成模型OmniGen：告別ControlNet、ipadapter等插件，僅憑提示即可控制影像生成與編輯](https://mp.weixin.qq.com/s/48HmqRGBOK1uBdzlprdKSA)


## Digital Human (虛擬數字人)
- [Linly-Talker](https://github.com/Kedreamix/Linly-Talker)：an intelligent AI system that combines large language models (LLMs) with visual models to create a novel human-AI interaction method. 
- [EchoMimicV2](https://github.com/antgroup/echomimic_v2)：[CVPR 2025] EchoMimicV2: Towards Striking, Simplified, and Semi-Body Human Animation
- [Hallo3](https://github.com/fudan-generative-vision/hallo3)：[CVPR 2025] Highly Dynamic and Realistic Portrait Image Animation with Diffusion Transformer Networks
- [MimicTalk](https://github.com/yerfor/MimicTalk)：[NeurIPS 2024] MimicTalk: Mimicking a personalized and expressive 3D talking face in minutes
- [JoyGen](https://github.com/JOY-MM/JoyGen)：Audio-Driven 3D Depth-Aware Talking-Face Video Editing
- [Latentsync](https://github.com/bytedance/LatentSync)
- [MuseTalk](https://github.com/TMElyralab/MuseTalk)



## Image Recognition (圖像識別)

- [ViT（Vision Transformer）解析](https://zhuanlan.zhihu.com/p/445122996)：https://github.com/google-research/vision_transformer

- [2040張圖片訓練出的ViT，準確率96.7%，連遷移表現都令人驚訝](https://zhuanlan.zhihu.com/p/463608959)

- [Swin Transformer: 用CNN的方式打敗CNN](https://zhuanlan.zhihu.com/p/362690149)：https://github.com/microsoft/Swin-Transformer

- [EfficientNetV2震撼發布！更小的模型，更快的訓練](https://zhuanlan.zhihu.com/p/361873583)：https://github.com/d-li14/efficientnetv2.pytorch

## Optical Character Recognition (光學文字識別)

**[針對物件或場景影像進行分析與偵測](https://www.twman.org/AI/CV)**
- 2025-03-03：[olmocr](https://github.com/allenai/olmocr)：[🚀本地部署最强OCR大模型olmOCR！支持结构化精准提取复杂PDF文件内容！](https://www.aivi.fyi/llms/deploy-olmOCR)
- 2025-02-05：[MinerU](https://github.com/opendatalab/MinerU)：[將PDF轉換為機器可讀格式的神器](https://mp.weixin.qq.com/s/ci5wp6gICTCtaRZfn5yWUQ)
- 2024-12-15：[markitdown](https://github.com/microsoft/markitdown)
- 2024-09-22：[OCR2.0时代-GOT来啦！](https://mp.weixin.qq.com/s/W-Ult-F3pU6Wvx3fHEN8yA)
- 2024-09-11：[GOT-OCR-2.0模型开源](https://mp.weixin.qq.com/s/rQL-Q0TGhT6e8Ti4zZalrg)
- 2024-08-20：[萬物皆可AI化！剛開源就有12000人圍觀的OCR 掃描PDF 開源工具！還可轉換為MarkDown！](https://www.53ai.com/news/MultimodalLargeModel/2024082059736.html)
- [advancedliteratemachinery/OCR/OmniParser](https://github.com/AlibabaResearch/AdvancedLiterateMachinery/tree/main/OCR/OmniParser)
- 2024-10-29：[Alibaba出品:OmniParser通用文檔複雜場景下OCR抽取](https://mp.weixin.qq.com/s/_1Aatpna7poIVRhfYk4aAQ)
- [RapidOCR](https://github.com/RapidAI/RapidOCR/blob/main/docs/README_zh.md)
- [12個流行的開源免費OCR項目](https://mp.weixin.qq.com/s/7EuhnQedAX6injBL_Dg_sQ)
- [用PaddleOCR的PPOCRLabel來微調醫療診斷書和收據](https://blog.twman.org/2023/07/wsl.html)
- [TableStructureRec: 表格結構辨識推理庫來了](https://zhuanlan.zhihu.com/p/668484933)：https://github.com/RapidAI/TableStructureRec

## Document Understanding (文件理解)

[Geewook Kim, Teakgyu Hong, Moonbin Yim, JeongYeon Nam, Jinyoung Park, Jinyeong Yim, Wonseok Hwang, Sangdoo Yun, Dongyoon Han, Seunghyun Park, "OCR-free Document Understanding Transformer", arXiv preprint, arXiv:2111.15664, 2022.](./donut.md)

## Document Layout Analysis (文件結構分析)

[Zejiang Shen, Ruochen Zhang, Melissa Dell, Benjamin Charles Germain Lee, Jacob Carlson, Weining Li, "A unified toolkit for Deep Learning Based Document Image Analysis", arXiv preprint, arXiv:2103.15348, 2021.](./LayoutParser.md)

<details open>
<summary><strong>LayoutLM series</strong></summary>

- **arXiv-2020**:[Yiheng Xu,Minghao Li, Lei Cui, Shaohan Huang, Furu Wei, Ming Zhou,"LayoutLM: Pre-training of Text and Layout for Document Image Understanding",arXiv:1912.13318, 2020](./LayoutLM.md)
- **arXiv-2021**:[Yang Xu, Yiheng Xu, Tengchao Lv, Lei Cui, Furu Wei, Guoxin Wang, Yijuan Lu, Dinei Florencio, Cha Zhang, Wanxiang Che, Min Zhang, Lidong Zhou,"LayoutLMv2: Multi-modal Pre-training for Visually-Rich Document Understanding",arXiv:2012.14740, 2021](./LayoutLMv2.md)
- **arXiv-2021**:[Yiheng Xu, Tengchao Lv, Lei Cui, Guoxin Wang, Yijuan Lu, Dinei Florencio, Cha Zhang, Furu Wei, "LayoutXLM: Multimodal Pre-training for Multilingual Visually-rich Document Understanding", arXiv:2104.08836](./LayoutXLM.md)
- **arXiv-2022**:[Yupan Huang, Tengchao Lv, Lei Cui, Yutong Lu and Furu Wei, "LayoutLMv3: Pre-training for Document AI with Unified Text and Image Masking", arXiv preprint, arXiv:2204.08387, 2022.](./LayoutLMv3.md)
</details>

[Geewook Kim, Teakgyu Hong, Moonbin Yim, Jeongyeon Nam, Jinyoung Park, Jinyeong Yim, Wonseok Hwang, Sangdoo Yun, Dongyoon Han, Seunghyun Park,"OCR-free Document Understanding Transformer",arXiv:2111.15664,2022](./donut.md)

[Minghao Li, Tengchao Lv, Lei Cui, Yijuan Lu, Dinei Florencio, Cha Zhang, Zhoujun Li and Furu Wei, "TrOCR: Transformer-based Optical Character Recognition with Pre-trained Models", arXiv preprint, arXiv:2109.10282, 2021](./TrOCR.md)

[Junlong Li, Yiheng Xu, Tengchao Lv, Lei Cui, Cha Zhang and Furu Wei, "DiT: Self-supervised Pre-training for Document Image Transformer", arXiv preprint, arXiv:2203.02378, 2022.](./DiT.md) 

## Text Recognition (文字識別)
Lukas Blecher, Guillem Cucurull, Thomas Scialom and Robert Stojnic, "Nougat: Neural Optical Understanding for Academic Documents", arXiv:2308.13418, 2023.
https://facebookresearch.github.io/nougat/
https://www.jiqizhixin.com/articles/2023-08-30-3

[Shancheng Fang, Hongtao Xie, Yuxin Wang, Zhendong Mao, Yongdong Zhang, "Read Like Humans: Autonomous, Bidirectional and Iterative Language Modeling for Scene Text Recognition", arXiv:2103.06495, 2021.](./ABINet.md)

[Shancheng Fang, Zhendong Mao, Hongtao Xie, Yuxin Wang, Chenggang Yan, Yongdong Zhang,"ABINet++: Autonomous, Bidirectional and Iterative Language Modeling for Scene Text Spotting",arXiv:2211.10578, 2022](./ABINet%2B%2B.md)

[Yuliang Liu, Chunhua Shen, Lianwen Jin, Tong He, Peng Chen, Chongyu Liu, Hao Chen, "ABCNet v2: Adaptive Bezier-Curve Network for Real-time End-to-end Text Spotting", arXiv preprint, 	arXiv:2105.03620, 2021.](./ABCNet_v2.md)

[Yongkun Du, Zhineng Chen, Caiyan Jia, Xiaoting Yin, Tianlun Zheng, Chenxia Li, Yuning Du, Yu-Gang Jiang, "SVTR: Scene Text Recognition with a Single Visual Model", arXiv:2205.00159,2022](./SVTR.md)

## DeepFake Detection (深度偽造偵測)
H. Zhao, et al., "Multi-attentional Deepfake Detection", Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition (CVPR), 2021, Nashville, TN, USA, 2021, pp. 2185-2194.


Sun, Zekun and Han, Yujie and Hua, Zeyu and Ruan, Na and Jia, Weijia, "Improving the Efficiency and Robustness of Deepfakes Detection through Precise Geometric Features", Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition (CVPR), 2021.

Xiangyu Zhu, Hao Wang, Hongyan Fei, Zhen Lei, and Stan Z. Li, "Face Forgery Detection by 3D Decomposition", Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition (CVPR), 2021.
