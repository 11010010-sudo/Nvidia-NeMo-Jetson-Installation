# Installing Nvidia-NeMo on Jetson Devices

## Introduction
NVIDIA NeMo is a conversational AI toolkit built for researchers working on automatic speech recognition (ASR), natural language processing (NLP), and text-to-speech synthesis (TTS).

### Initial System Packages Required By Nemo
```python
    sudo apt-get update && upgrade
    sudo apt-get install libhdf5-serial-dev hdf5-tools libhdf5-dev zlib1g-dev
    sudo apt-get install zip libjpeg8-dev liblapack-dev libblas-dev gfortran
    sudo apt-get install libopenblas-base libopenmpi-dev
    sudo apt-get install -y libiconv-hook-dev
    sudo apt-get install -y libsndfile1 ffmpeg
    sudo apt-get install libmecab-dev
    sudo apt install curl
    sudo apt install sox
    sudo apt-get install protobuf-compiler libprotoc-dev
    sudo apt-get install python-pyaudio python3-pyaudio
    sudo apt-get install sox libsndfile1 ffmpeg portaudio19-dev
```
### Setting-Up Virtual Environment
```python
    sudo apt-get install python3-dev python3-pip
    pip3 install -U virtualenv
    python3 -m virtualenv --system-site-packages /home/<Username>/python
```

### Activate Virtual Environment
```python
    source /home/<Username>/python/bin/activate
```
#### Setup Virtual-Environment
```python
    sudo apt-get update
    sudo apt-get install python3-pip
```

### Start to Build Pip Packages That are Not Present in The NeMo-toolkit
```python
    pip install testresources
    pip install setuptools
    pip install --upgrade setuptools
    pip install Cython
    python3 -m pip install sounddevice
    pip install pyaudio
```
### Building Wheel for Tokenizer and llvmlite from source

1. Install Rust Compiler for Tokenizer
```python
    curl --proto ‘=https’ --tlsv1.2 -sSf https://sh.rustup.rs | sh
```
2. After Install Restart Terminal
```python
    source $HOME/.cargo/env
```
3. Install Transformer
```python
    pip install transformers
```
### Build LLVM From Source
```python
    wget https://github.com/llvm/llvm-project/releases/download/llvmorg-9.0.1/llvm-9.0.1.src.tar.xz
```
#### Unzip Files then Go to folders
```python
    cd llvm-9.0.1.src/
    mkdir build
    cd build
    cmake ../ -DCMAKE_BUILD_TYPE=Release -DLLVM_TARGETS_TO_BUILD=”ARM;X86;AArch64”
    make -j8
    sudo make install
    sudo ldconfig
    pip install git+https://github.com/jschueller/llvmlite.git@patch-1
```
### Finally Run the Nemo-toolkit
```python
    pip install nemo_toolkit[all]
```

## Additional Setup & Configuration
### Build Apex From Source
```python
    git clone https://github.com/NVIDIA/apex
    cd apex
    pip install -v --disable-pip-version-check --no-cache-dir ./
```
### Build OnnxRuntime-GPU from Source
```python
    wget https://nvidia.box.com/s/bfs688apyvor4eo8sf3y1oqtnarwafww -O onnxruntime_gpu-1.8.0-cp36-cp36m-linux_aarch64.whl
    pip3 install onnxruntime_gpu-1.8.0-cp36-cp36m-linux_aarch64.whl
```
