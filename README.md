# RAG with LlamaIndex - Nvidia CUDA + WSL (Windows Subsystem for Linux) + Word documents + Local LLM

These notebooks demonstrate the use of LlamaIndex for Retrieval Augmented Generation using Windows WSL and an Nvidia's CUDA.

Environment:
- Windows 11
- Anaconda environment
- Nvidia RTX 3090
- LLMs - Mistral 7B, Llama 2 13B Chat - Quantized versions

Your Data:
- Add Word documents to the "Data" folder for the RAG to use

Package versions:
- See the "conda_package_versions.txt" for the full list of versions in the conda environment (generated using "conda list").
- See/utilise the "requirements.txt" file (note that you need to have installed the CUDA Toolkit using the instructions below, the versions are very important).

Local LLMs:
- Put your downloaded LLM files into a "Models" folder
- I downloaded the quantized versions of the LLMs from huggingface.co - thanks to TheBloke who provided these quantized GGUF models. You can use higher quantized versions or different LLMs - just be aware that LLMs may have different prompt templates so be sure to use the correct prompt template format (e.g. Llama 2 requires a specific format for best results - see the Llama code for a function that creates the prompt).
- https://huggingface.co/TheBloke/Mistral-7B-Instruct-v0.1-GGUF
- https://huggingface.co/TheBloke/Llama-2-13B-chat-GGUF

Important libraries to "pip install":
- llama-cpp-python
- transformers
- llama-index
- docx2txt
- sentence-transformers

Notes:
Getting the Nvidia CUDA libraries installed correctly for use within WSL was challenging, I followed the steps from these two links:

1. CUDA Toolkit version 12.3 (latest as of 2023-11-03)
- https://docs.nvidia.com/cuda/wsl-user-guide/index.html
2. Install instructions within WSL:
- https://developer.nvidia.com/cuda-downloads?target_os=Linux&target_arch=x86_64&Distribution=WSL-Ubuntu&target_version=2.0&target_type=deb_local

To tell if you are utilising your Nvidia graphics card, in your command prompt, while in the conda environment, type "nvidia-smi". You should see your graphics card and you're notebook is running you should see your utilisation increase.