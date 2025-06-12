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
cd /home/limengkui/project
docker run --rm --shm-size=2g -it --name=tensorrt -e HF_ENDPOINT="https://hf-mirror.com" -v $PWD:/workspace --entrypoint /bin/bash --gpus all project_cnn_llm_yolo:v0
conda activate cnn
cd /workspace/tensorrt_cnn/
bash resnet50_fp16.sh
bash resnet50_int8.sh

bash mobilenetv2_fp16.sh
bash mobilenetv2_int8.sh
```

2. run llm(llama、bert)
```
cd /home/limengkui/project
docker run --rm --shm-size=2g -it --name=tensorrt -e HF_ENDPOINT="https://hf-mirror.com" -v $PWD:/workspace --entrypoint /bin/bash --gpus all project_cnn_llm_yolo:v0
conda activate llama
cd /workspace/llm/TensorRT-LLM/examples/llama/test
bash mmlu_test.sh(include fp16 & int8)

conda activate bert
cd /workspace/llm/TensorRT-LLM/examples/bert
bash run_squad.sh(include fp16 & int8)
```

3. run vits(vit、swin、tnt)
```
cd /home/limengkui/project
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

4. run yolo(yolov5、yolov7、yolov10、yolo-world)
```
cd /home/limengkui/project
docker run --rm --shm-size=2g -it --name=tensorrt -e HF_ENDPOINT="https://hf-mirror.com" -v $PWD:/workspace --entrypoint /bin/bash --gpus all project_cnn_llm_yolo:v0
conda activate yolos
cd /workspace/YOLO/v5qat
bash run_yolov5_fp16.sh
bash run_yolov5_int8.sh

cd /workspace/YOLO/v7qat
bash run_yolov7_fp16.sh
bash run_yolov7_int8.sh

cd /workspace/YOLO/v10qat
bash run_yolov10_fp16.sh
bash run_yolov10_int8.sh

cd /workspace/YOLO/worldqat
bash run_yoloworld_fp16.sh
bash run_yoloworld_int8.sh

```






