[Yupan Huang, Tengchao Lv, Lei Cui, Yutong Lu and Furu Wei, "LayoutLMv3: Pre-training for Document AI with Unified Text and Image Masking", arXiv preprint, arXiv:2204.08387, 2022.](https://arxiv.org/pdf/2204.08387)

[github](https://aka.ms/layoutlmv3)

[PaperWithCode](https://paperswithcode.com/paper/layoutlmv3-pre-training-for-document-ai-with)

## Abstract

Self-supervised pre-training techniques have achieved remarkable progress in Document AI. Most multimodal pre-trained models use a masked language modeling objective to learn bidirectional representations on the text modality, but they differ in pre-training objectives for the image modality. This discrepancy adds difficulty to multimodal representation learning. In this paper, we propose LayoutLMv3 to pre-train multimodal Transformers for Document AI with unified text and image masking. Additionally, LayoutLMv3 is pre-trained with a word-patch alignment objective to learn cross-modal alignment by predicting whether the corresponding image patch of a text word is masked. The simple unified architecture and training objectives make LayoutLMv3 a general-purpose pre-trained model for both text-centric and image-centric Document AI tasks. Experimental results show that LayoutLMv3 achieves state-of-the-art performance not only in text-centric tasks, including form understanding, receipt understanding, and document visual question answering, but also in image-centric tasks such as document image classification and document layout analysis. The code and models are publicly available at this https URL. https://aka.ms/layoutlmv3

