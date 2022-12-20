# LISA: Localized Image Stylization with Audio via Implicit Neural Representation
![lisa_main](https://user-images.githubusercontent.com/44921488/208412208-1a0dc030-91de-4bca-8ac8-14add13bc4e0.png)
Paper: [arXiv](https://arxiv.org/pdf/2211.11381.pdf)  
Seung Hyun Lee*, Chanyoung Kim*, Wonmin Byeon, Sang Ho Yoon, Jinkyu Kim†, and Sangpil Kim†    
  
Abstract: *We present a novel framework, Localized Image Stylization with Audio **LISA** which performs audio-driven localized image stylization. 
    Sound often provides information about the specific context of the scene and is closely related to a certain part of the scene or object. However, existing image stylization works have focused on stylizing the entire image using an image or text input. Stylizing a particular part of the image based on audio input is natural but challenging.
    In this work, we propose a framework that a user provides an audio input to localize the sound source in the input image and another for locally stylizing the target object or scene. LISA first produces a delicate localization map with an audio-visual localization network by leveraging CLIP embedding space. We then utilize implicit neural representation~(INR) along with the predicted localization map to stylize the target object or scene based on sound information. The proposed INR can manipulate the localized pixel values to be semantically consistent with the provided audio input.
    Through a series of experiments, we show that the proposed framework outperforms the other audio-guided stylization methods. Moreover, LISA constructs concise localization maps and naturally manipulates the target object or scene in accordance with the given audio input.*
## Getting Started
### Installation
- Follow the steps below:
```bash
$ conda create -n lisa python=3.8
$ conda install pytorch==1.11.0 torchvision==0.12.0 torchaudio==0.11.0 cudatoolkit=11.3 -c pytorch
$ conda install --yes -c pytorch pytorch=1.7.1 torchvision cudatoolkit=11.0
$ pip install ftfy regex tqdm
$ pip install git+https://github.com/openai/CLIP.git
```
### Download Pretrained Weight
```bash
$ cd LISA
$ mkdir weights
```
Download Link : [AudioEncoder](https://drive.google.com/file/d/14JDadJLdQ3vBGLKraW-nfyIlb1-rqoJ2/view?usp=sharing), [CLIPSeg](https://drive.google.com/file/d/1N0q5czPMf1VS_CJdSFdZowhSkNNwY9KR/view?usp=sharing)  
Place downloaded weights under "./weights" folder.

## Method
### Audio-Visual Localizer
![image](https://user-images.githubusercontent.com/44921488/208580210-f4e19640-fb6b-4a43-873b-59e573e31b8b.png)
An overview of our Audio-visual Localizer, which identifies an image region corresponding to the sound input (e.g., localizing a train based on a sound of engine noise), producing a probability mask as an output. Due to the lack of data to provide such supervision, we leverage the existing text-guided zero-shot segmentation model, using its output as a pseudo label.

### Localized Image Stylization with Audio (LISA)
![image](https://user-images.githubusercontent.com/44921488/208580310-7100e562-9e8a-41f4-beba-23646af8af25.png)
An overview of our proposed method called Localized Image Stylization with Audio (LISA). Our model consists of two main parts: (i) Audio-Visual Localizer, which outputs a pixel-level localization mask conditioned on an audio input (e.g., given a sound of engine noise input, our model localizes a train from the source image, producing a probability mask) and (ii) Audio-Guided INR Stylizer, which outputs stylized images by taking pixel locations as input and producing RGB pixel values as output. Conditioned on a new user-provided sound input (e.g., splashing plastic bag), our model is optimized with multi-scale PatchCLIP loss to generate an audio-guided “locally” stylized image. We also use Foreground Regularization Loss to make the stylized image and a source image perceptually look similar.


## Training Stylization
### Localizing with text condition
#### Stylizing with audio
```bash
$ python train_text_audio.py --content_path "./test_set/chicago.jpg" --content_name "buildings" --audio_path "./audiosample/fire.wav"
```
#### Stylizing with text
```bash
$ python train_text_text.py --content_path "./test_set/church.jpeg" --content_name "church" --text "wood"
```

## Results
### Sound Source Localization
|Method|CIoU|AUC|
|---|---|---|
|LVS (CVPR2021)|73.59%|59.00%|
|EZ-VSL (ECCV2022)|83.94%|63.60%|
|Ours|**85.94%**|**66.70%**|
### Localized Stylization Result
![image](https://user-images.githubusercontent.com/44921488/208580509-a8deaf13-83db-4fec-9fc4-b50fd8ce95ca.png)
