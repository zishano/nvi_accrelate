# nvi_accrelate
3090、4090、A100加速cnn、vit、yolo、llm

## Updates
* **`5.30, 2025`**: Update: We accomplished base
* **

## Install
1. Setting docker(3090、4090、A100)
```
docker pull docker push zishanozty/project_3090:v0
docker load -i test_3090.tar
docker run --rm --shm-size=2g -it --name=tensorrt -e HF_ENDPOINT="https://hf-mirror.com" -v $PWD:/workspace --entrypoint /bin/bash --gpus all 3090:v0
docker run --rm --shm-size=2g -it --name=tensorrt -e HF_ENDPOINT="https://hf-mirror.com" -v $PWD:/workspace --entrypoint /bin/bash --gpus '"device=1"' 3090:v0
```

2. Clone the repository
```
git clone https://github.com/zishanozty/nvi_accrelate
cd workspace
```

## How to use 
1. run cnn(resnet50、mobilenetv2)
```
conda activate cnn
cd /workspace/tensorrt_cnn/
bash resnet50_save.sh
bash resnet50_fp32.sh
bash resnet50_fp16.sh
bash resnet50_int8.sh

bash mobilenetv2_save.sh
bash mobilenetv2_fp32.sh
bash mobilenetv2_fp16.sh
bash mobilenetv2_int8.sh
```

2. run yolo(yolov5、yolov10、yolo-world)
```
conda activate yolo
cd /workspace/yolo-models/
python run.py gen
python run.py eval
```

4. run llm(llama、bert)
```
conda activate llama
cd /workspace/llm/TensorRT-LLM/examples/llama/test
bash mmlu_test.sh
conda activate bert
cd /workspace/llm/TensorRT-LLM/examples/bert
bash run_squad.sh
```


