# RVC Text-to-Speech WebUI

This is a text-to-speech Gradio webui for [RVC](https://github.com/RVC-Project/Retrieval-based-Voice-Conversion-WebUI) models, using [edge-tts](https://github.com/rany2/edge-tts).

[🤗 Online Demo](https://huggingface.co/spaces/litagin/rvc_okiba_TTS)

This can run on CPU without GPU (but slow).

![Screenshot](assets/screenshot.jpg)

## INFO

This is a fork of the original repo intended to run in Colab.

{
"nbformat": 4,
"nbformat_minor": 0,
"metadata": {
"colab": {
"provenance": [],
"gpuType": "T4",
"authorship_tag": "ABX9TyPhu2JwUWluSKorHEpyTi5w",
"include_colab_link": true
},
"kernelspec": {
"name": "python3",
"display_name": "Python 3"
},
"language_info": {
"name": "python"
},
"accelerator": "GPU"
},
"cells": [
{
"cell_type": "markdown",
"metadata": {
"id": "view-in-github",
"colab_type": "text"
},
"source": [
"<a href=\"https://colab.research.google.com/gist/cmooredev/b7a9e627a182e7cce20b870aceff22fc/copy-of-rvcttswebui.ipynb\" target=\"_parent\"><img src=\"https://colab.research.google.com/assets/colab-badge.svg\" alt=\"Open In Colab\"/></a>"
]
},
{
"cell_type": "code",
"execution_count": null,
"metadata": {
"id": "VQEOzs7Emp7f"
},
"outputs": [],
"source": [
"# Clone the repo\n",
"!git clone https://github.com/cmooredev/rvc-tts-webui.git\n",
"%cd rvc-tts-webui\n",
"\n",
"# Download the model files\n",
"!curl -L -O https://huggingface.co/lj1995/VoiceConversionWebUI/resolve/main/hubert_base.pt\n",
"!curl -L -O https://huggingface.co/lj1995/VoiceConversionWebUI/resolve/main/rmvpe.pt\n"
]
},
{
"cell_type": "code",
"source": [
"# Install requirements\n",
"!pip install -r requirements.txt"
],
"metadata": {
"id": "Z2mL0i7sntnR"
},
"execution_count": null,
"outputs": []
},
{
"cell_type": "code",
"source": [
"%run app.py"
],
"metadata": {
"id": "ZfD8b99Vmr5n"
},
"execution_count": null,
"outputs": []
}
]
}

## Install

Requirements: Tested for Python 3.10 on Windows 11. Python 3.11 is probably not supported, so please use Python 3.10.

```bash
git clone https://github.com/litagin02/rvc-tts-webui.git
cd rvc-tts-webui

# Download models in root directory
curl -L -O https://huggingface.co/lj1995/VoiceConversionWebUI/resolve/main/hubert_base.pt
curl -L -O https://huggingface.co/lj1995/VoiceConversionWebUI/resolve/main/rmvpe.pt

# Make virtual environment
python -m venv venv
# Activate venv (for Windows)
venv\Scripts\activate

# Install PyTorch manually if you want to use NVIDIA GPU (Windows)
# See https://pytorch.org/get-started/locally/ for more details
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118

# Install requirements
pip install -r requirements.txt
```

## Locate RVC models

Place your RVC models in `weights/` directory as follows:

```bash
weights
├── model1
│   ├── my_model1.pth
│   └── my_index_file_for_model1.index
└── model2
    ├── my_model2.pth
    └── my_index_file_for_model2.index
...
```

Each model directory should contain exactly one `.pth` file and at most one `.index` file. Directory names are used as model names.

It seems that non-ASCII characters in path names gave faiss errors (like `weights/モデル1/index.index`), so please avoid them.

## Launch

```bash
# Activate venv (for Windows)
venv\Scripts\activate

python app.py
```

## Update

```bash
git pull
venv\Scripts\activate
pip install -r requirements.txt --upgrade
```

## Troubleshooting

```
error: Microsoft Visual C++ 14.0 or greater is required. Get it with "Microsoft C++ Build Tools": https://visualstudio.microsoft.com/visual-cpp-build-tools/
      [end of output]

  note: This error originates from a subprocess, and is likely not a problem with pip.
  ERROR: Failed building wheel for fairseq
Failed to build fairseq
ERROR: Could not build wheels for fairseq, which is required to install pyproject.toml-based projects
```

Maybe fairseq needs Microsoft C++ Build Tools.
[Download installer](https://visualstudio.microsoft.com/ja/thank-you-downloading-visual-studio/?sku=BuildTools&rel=16) and install it.
