# Environment configuration

1. create conda environment

```bash
conda create -n dvc python=3.10
```
then activate conda environment

```bash
conda activate dvc
```

2. install torch 2.1.2, NVCC version == 12.1

```bash
conda install pytorch==2.1.2 torchvision==0.16.2 torchaudio==2.1.2 pytorch-cuda=12.1 -c pytorch -c nvidia
```

3. install tensorflow

```bash
pip install tensorflow
```
