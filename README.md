[# llama-server-examples

## Project Setup

```shell
poetry shell
poetry install
```

## Run Models Llama ZMQ Server

### Download GGUF Models

```shell
huggingface-cli download TheBloke/vicuna-7B-v1.5-GGUF vicuna-7b-v1.5.Q4_K_M.gguf --local-dir ./models/vicuna-7B-v1.5-GGUF --local-dir-use-symlinks False
```

```shell
huggingface-cli download TheBloke/Mistral-7B-Instruct-v0.1-GGUF mistral-7b-instruct-v0.1.Q4_K_M.gguf --local-dir ./models/Mistral-7B-Instruct-v0.1-GGUF --local-dir-use-symlinks False
```

### Run Vicuna Model CPU

```shell
docker run --rm -it -p 5555:5555 \
-e MODEL_FILE=vicuna-7B-v1.5-GGUF/vicuna-7b-v1.5.Q4_K_M.gguf \
-e NUM_THREADS=6 \
-e CONTEXT_SIZE=2048 \
-v ./models:/app/models \
qimia/llama-zmq-server:9cdd3098
```

### Run Mistral Model CPU

```shell
docker run --rm -it -p 5555:5555 \
-e MODEL_FILE=Mistral-7B-Instruct-v0.1-GGUF/mistral-7b-instruct-v0.1.Q4_K_M.gguf \
-e NUM_THREADS=6 \
-e CONTEXT_SIZE=2048 \
-v ./models:/app/models \
qimia/llama-zmq-server:9cdd3098
```

### Run Vicuna Model GPU

```shell
docker run --rm -it -p 5555:5555 --runtime=nvidia --gpus 1 \
-e MODEL_FILE=vicuna-7B-v1.5-GGUF/vicuna-7b-v1.5.Q4_K_M.gguf \
-e NUM_THREADS=6 \
-e CONTEXT_SIZE=2048 \
-e NUM_GPU_LAYERS=200000 \
-v ./models:/app/models \
qimia/llama-zmq-server-cuda:e8c4e424
```

### Run Mistral Model GPU

```shell
docker run --rm -it -p 5555:5555 --runtime=nvidia --gpus 1 \
-e MODEL_FILE=Mistral-7B-Instruct-v0.1-GGUF/mistral-7b-instruct-v0.1.Q4_K_M.gguf \
-e NUM_THREADS=6 \
-e CONTEXT_SIZE=2048 \
-e NUM_GPU_LAYERS=200000 \
-v ./models:/app/models \
qimia/llama-zmq-server-cuda:e8c4e424
```