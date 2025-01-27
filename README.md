# The-Emergence-of-Objectness
This is the official released code for our paper, [The Emergence of Objectness: Learning Zero-Shot Segmentation from Videos](https://arxiv.org/abs/2111.06394), which has been accepted by NeurIPS 2021. Code will be available soon. 

# Slide
Our slide is available at:
https://drive.google.com/file/d/1iM6mHTHWssl8Q3vqbsW0fC4Pqki-UbfM/view?usp=sharing

# Code
To be released soon after the conference. 

# Abstract
Humans can easily segment moving objects without knowing what they are. That objectness could emerge from continuous visual observations motivates us to model grouping and movement concurrently from unlabeled videos. Our premise is that a video has different views of the same scene related by moving components, and the right region segmentation and region flow would allow mutual view synthesis which can be checked from the data itself without any external supervision. 

Our model starts with two separate pathways: an appearance pathway that outputs feature-based region segmentation for a single image, and a motion pathway that outputs motion features for a pair of images. It then binds them in a conjoint representation called segment flow that pools flow offsets over each region and provides a gross characterization of moving regions for the entire scene. By training the model to minimize view synthesis errors based on segment flow, our appearance and motion pathways learn region segmentation and flow estimation automatically without building them up from low-level edges or optical flows respectively. 

Our model demonstrates the surprising emergence of objectness in the appearance pathway, surpassing prior works on zero-shot object segmentation from an image, moving object segmentation from a video with unsupervised test-time adaptation, and semantic image segmentation by supervised fine-tuning. Our work is the first truly end-to-end zero-shot object segmentation from videos. It not only develops generic objectness for segmentation and tracking, but also outperforms prevalent image-based contrastive learning methods without augmentation engineering.

# Approach 
![image](https://user-images.githubusercontent.com/45531420/141472988-2618129e-1bee-4a12-af91-0498566f3b6f.png)
We learn a single-image segmentation network and a dual-frame motion network with an unsupervised image reconstruction loss. We sample two frames, $i$ and $j$, from a video. Frame $i$ goes through the segmentation network and outputs a set of masks, whereas frames $i$ and $j$ go through the motion network and output a feature map. The feature is pooled per mask and a flow is predicted. All the segments and their flows are combined into a segment flow representation from frame $i$ → $j$, which are used to warp frame $i$ into $j$, and compared against frame $j$ to train the two networks.

# Zero-Shot Saliency Detection
![image](https://user-images.githubusercontent.com/45531420/141473099-c36d807f-4a34-4818-b185-f8c7f44aec47.png)
Qualitative salient object detection results. We directly transfer our pretrained segmentation network to novel images on the DUTS dataset without any finetuning. Surprisingly, we find that the model pretrained on videos to segment moving objects can generalize to detect stationary unmovable objects in a static image, e.g. the statue, the plate, the bench and the tree in the last column.

# Zero-shot Video Object Segmentation
## Qualitative results of SegTrackv2
![image](https://user-images.githubusercontent.com/45531420/141473734-2c273d96-d9a5-42f3-9372-667d873f483c.png)

## Qualitative results of DAVIS 2016
![image](https://user-images.githubusercontent.com/45531420/141473806-8566300c-e399-409c-98b9-11b06483c76f.png)

## Qualitative results of FBMS59
![image](https://user-images.githubusercontent.com/45531420/141473838-ea03d3e9-5c02-4c83-b750-10ed9588a537.png)

