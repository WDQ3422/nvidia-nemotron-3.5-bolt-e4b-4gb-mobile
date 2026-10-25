# NVIDIA Nemotron 3.5 Bolt E4B 4GB 手机部署（Termux）

本文记录在 Android 设备上通过 Termux 编译 `llama.cpp` 并运行 NVIDIA Nemotron 3.5 Bolt E4B 4GB GGUF 模型的步骤。

## 1. 安装 F-Droid 和 Termux

1. 从 [F-Droid](https://f-droid.org) 安装 F-Droid。
2. 在 F-Droid 中安装 Termux。
3. 打开 Termux。

## 2. 获取存储权限并安装依赖

```bash
termux-setup-storage
pkg update && pkg upgrade -y
pkg install -y git cmake make clang wget curl libandroid-spawn
```

## 3. 克隆并编译 llama.cpp

```bash
cd ~
git clone https://github.com/ggml-org/llama.cpp
cd llama.cpp
cmake -B build -DCMAKE_BUILD_TYPE=Release
cmake --build build --config Release -j 4
```

## 4. 下载模型

从 Hugging Face 下载模型：

<https://huggingface.co/nvidia/NVIDIA-Nemotron-3.5-Bolt-E4B-4GB/resolve/main/Nemotron-3.5-Bolt-E4B-Q4_K_M.gguf>

将下载的 `Nemotron-3.5-Bolt-E4B-Q4_K_M.gguf` 放到手机的 `Download` 目录。

## 5. 运行模型

```bash
cd ~/llama.cpp
./build/bin/llama-server -m ~/storage/downloads/Nemotron-3.5-Bolt-E4B-Q4_K_M.gguf -c 2048
```

## 原始备忘

完整原始文本见 [NVIDIA-Nemotron-3.5-Bolt-E4B-4GB手机部署gguf.txt](./NVIDIA-Nemotron-3.5-Bolt-E4B-4GB手机部署gguf.txt)。
