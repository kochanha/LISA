# LISA
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
## Training Stylization
### Localizing with text, stylizing with audio
```bash
$ python train_text_audio.py --content_path "./test_set/chicago.jpg" --content_name "buildings" --audio_path "./audiosample/fire.wav"
```
