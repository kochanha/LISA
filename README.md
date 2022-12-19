# LISA: Localized Image Stylization with Audio via Implicit Neural Representation
PDF: [arXiv](https://arxiv.org/pdf/2211.11381.pdf)
![lisa_main](https://user-images.githubusercontent.com/44921488/208412208-1a0dc030-91de-4bca-8ac8-14add13bc4e0.png)
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
