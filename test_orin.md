# nvi_accrelate
3090、4090、A100加速cnn、vit、yolo、llm

## Updates
* **`5.30, 2025`**: Update: We accomplished base
* **`6.10, 2025`**: Update 

## 0.Setup(⭐⭐⭐All ready!⭐⭐⭐)
1. Setting docker(3090、4090、A100)
```
docker pull docker push zishanozty/project_3090:v0
docker load -i test_3090.tar
docker run --rm --shm-size=2g -it --name=tensorrt -e HF_ENDPOINT="https://hf-mirror.com" -v $PWD:/workspace --entrypoint /bin/bash --gpus all 3090:v0
docker run --rm --shm-size=2g -it --name=tensorrt -e HF_ENDPOINT="https://hf-mirror.com" -v $PWD:/workspace --entrypoint /bin/bash --gpus '"device=1"' 3090:v0
docker run -it --rm --gpus=all "--cap-add=SYS_ADMIN" --shm-size=16g --ulimit memlock=-1  --ulimit stack=67108864 -v $PWD:/workspace vits:v0
```

2. Clone the repository
```
git clone https://github.com/zishanozty/nvi_accrelate
cd workspace
```

## 1.How to use(Accuray Test Results on 4090 & A100) 
1. run cnn(resnet50、mobilenetv2)
```
sudo mount -t exfat-fuse -o uid=1000,gid=1000,dmask=022,fmask=133 /dev/sda1 /media/qiyuan/F
cd /media/qiyuan/F/Task/qiyaun/total_project/project
sudo docker run --rm --shm-size=2g -it --name=tensorrt -e HF_ENDPOINT="https://hf-mirror.com" -v $PWD:/workspace --entrypoint /bin/bash --runtime=nvidia project_cnn:v0
cd /workspace/tensorrt_cnn/
bash resnet50_fp16.sh
bash resnet50_int8.sh

bash mobilenetv2_fp16.sh
bash mobilenetv2_int8.sh
```

2. run vits(vit、swin、tnt)
```
cd /media/qiyuan/F/Task/qiyaun/total_project/project
docker run -it --rm --gpus=all "--cap-add=SYS_ADMIN" --shm-size=16g --ulimit memlock=-1  --ulimit stack=67108864 -v $PWD:/workspace project_vits:v0
cd /workspace/FasterTransformer/examples/pytorch/vit
bash run_vit_fp16_accuracy.sh
bash run_vit_int8_accuracy.sh

cd /workspace/FasterTransformer/examples/pytorch/swin
bash run_swin_fp16_accuracy.sh
bash run_swin_int8_accuracy.sh

cd /home/limengkui/project
docker run --name test -it --rm --gpus all --network host --shm-size 16g -v $PWD:/workspace project_vits:v1
cd /workspace/Transformer-TensorRT
bash run_tnt_fp16_accuracy.sh
bash run_tnt_int8_accuracy.sh
```

4. run yolo(yolov5、yolov10、yolo-world)-⭐Todo
```
cd /workspace/yolo-models/
python run.py gen
python run.py eval
```






