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

# Prepare dataset

### Test data

This method only provide P-frame compression, so we first need to generate I frames by H.265. We take UVG dataset as an example.

1. Download [UVG dataset](http://ultravideo.cs.tut.fi/#testsequences_x)(1080p/8bit/YUV/RAW) to `data/UVG/videos/`.
2. Crop Videos from 1920x1080 to 1920x1024.
    ```
    cd data/UVG/
    ffmpeg -pix_fmt yuv420p  -s 1920x1080 -i ./videos/xxxx.yuv -vf crop=1920:1024:0:0 ./videos_crop/xxxx.yuv
    ```
3. Convert YUV files to images.
    ```
    python convert.py
    ```
4. Create I frames. We need to create I frames by H.265 with $crf of 20,23,26,29.
    ```
    cd CreateI
    sh h265.sh $crf 1920 1024
    ```
    After finished the generating of I frames of each crf, you need to use bpps of each video in `result.txt` to fill the bpps in Class UVGdataset in `dataset.py`.

## Training
    cd examples/example
    sh cp.sh
    sh run.sh
If you want models with more λ, you can edit `config.json`

If you want to use tensorboard:

    cd examples
    sh tf.sh xxxx

## Testing
Our pretrained model with λ=2048,1024,512,256 is provided on [Google Drive](https://drive.google.com/drive/folders/1M54MPrAzaA0QVySnzUu9HZWx1bfIrTZ6?usp=sharing). You can put it to `snapshot/` and run `test.sh`:

    sh test.sh
