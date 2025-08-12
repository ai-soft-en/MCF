# Multi-Sensor Collaborative Intelligence-Supported Meta Computing Framework for Intelligent Feeding in Industrial Aquaculture Systems

Implementation of paper - Review stage


## System Requirements
- **Operating System**: Ubuntu 20.04/22.04 (Recommended) or Windows 10/11 (WSL2 required)
- **GPU**: NVIDIA GPU (≥8GB VRAM recommended)
- **CUDA**: 11.3+ (Must match PyTorch version)
- **Python**: 3.8 or 3.9

## Installation Steps

  Clone Repository
```bash
git clone https://github.com/ai-soft-en/MCF.git
cd MCF
```

  Create Python Virtual Environment
```bash
python -m venv MSCISMCF
source MSCISMCF/bin/activate  # Linux
# or MSCISMCF\Scripts\activate  # Windows
```

  Install Dependencies
```bash
pip install --upgrade pip
pip install -r requirements.txt
```


## Training

Data preparation
git clone https://github.com/ai-soft-en/Demonstration-Dataset.git


Single GPU training

``` shell
# train p5 models
python train.py --workers 8 --device 0 --batch-size 32 --data data/fish.yaml --img 640 640 --cfg cfg/training/yolov7-fish.yaml --weights

# train p6 models
python train_aux.py --workers 8 --device 0 --batch-size 16 --data data/fish.yaml --img 1280 1280 --cfg cfg/training/yolov7-fish2.yaml --weights 
```

Multiple GPU training

``` shell
# train p5 models
python -m torch.distributed.launch --nproc_per_node 4 --master_port 9527 train.py --workers 8 --device 0,1,2,3 --sync-bn --batch-size 128 --data data/fish.yaml --img 640 640 --cfg cfg/training/yolov7-fish.yaml

# train p6 models
python -m torch.distributed.launch --nproc_per_node 8 --master_port 9527 train_aux.py --workers 8 --device 0,1,2,3,4,5,6,7 --sync-bn --batch-size 128 --data data/fish.yaml --img 1280 1280 --cfg cfg/training/yolov7-fish1.yaml
```

## Transfer learning

[`yolov7_fish.pt`](https://github.com/) [`yolov7x_fish.pt`](https://github.com/)



## Acknowledgements

<details><summary> <b>Expand</b> </summary>
  
* [https://github.com/WongKinYiu/yolov7](https://github.com/WongKinYiu/yolov7)
  
</details>
