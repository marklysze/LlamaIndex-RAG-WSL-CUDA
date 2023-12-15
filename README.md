# RAG with LlamaIndex - Nvidia CUDA + WSL (Windows Subsystem for Linux) + Word documents + Local LLM

These notebooks demonstrate the use of LlamaIndex for Retrieval Augmented Generation using Windows WSL and an Nvidia's CUDA.

Environment:
- Windows 11
- Anaconda environment
- Nvidia RTX 3090
- NVIDIA CUDA Toolkit Version 12.3
- 64GB RAM
- LLMs - Mistral 7B, Llama 2 13B Chat, Orca 2 13B, Yi 34B, Mixtral 8x7B - Quantized versions

**December 2023 Note: Update llama-cpp-python to v0.2.23 in order to run Mixtral 8x7B**

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
- https://huggingface.co/TheBloke/Orca-2-13B-GGUF
- https://huggingface.co/TheBloke/Yi-34B-Chat-GGUF
- https://huggingface.co/TheBloke/Mixtral-8x7B-Instruct-v0.1-GGUF

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

To tell if you are utilising your Nvidia graphics card, in your command prompt, while in the conda environment, type "nvidia-smi". You should see your graphics card and when you're notebook is running you should see your utilisation increase.

### Output examples

Question asked of the model based on the story:
> Summarise the story for me

**Mistral 7B:**
> The story follows Thundertooth, a talking dinosaur who has found a new home in a futuristic city. He is embraced by the citizens and finds purpose beyond merely satisfying his hunger. With the help of the city's brilliant engineers, he founded a toy factory that produces magical, interactive toys. As the years pass, Thundertooth meets a kind dinosaur named Seraphina and starts a family. Together, they explore the city and find a sustainable solution to satisfy Thundertooth's hunger without compromising the well-being of the citizens. The story highlights the importance of understanding and cooperation in overcoming challenges.

**Llama 2:**
> Of course! Here's a summary of the story based on the provided sources:
>
> Thundertooth, a talking dinosaur from prehistoric times, was transported through a time portal to a futuristic city. He found himself in a world filled with advanced technology and modern marvels, but he struggled to find food to satisfy his hunger. The city's inhabitants, led by Mayor Grace, welcomed Thundertooth and worked together to find a solution to his predicament.
>
> With the help of the city's engineers, Thundertooth founded a unique toy factory that produced magical widgets that captured the hearts of both children and adults. He started a family with a kind and intelligent dinosaur named Seraphina, and they had four children who each possessed unique characteristics.
>
> When a massive meteor threatened the city, Thundertooth joined forces with Mayor Grace and the leading scientists to find a way to divert or neutralize the threat. With his intelligence and resourcefulness, Thundertooth became an integral part of the team and helped save the city from disaster.
>
> That's the gist of the story! Is there anything else you'd like to know?

**Orca 2:**
> The story is about Thundertooth, a dinosaur who travels from prehistoric times to a futuristic city. He meets Mayor Grace and her people, who help him find a new home and a purpose. He creates a toy factory that makes amazing widgets, and falls in love with Seraphina, another dinosaur. Together they have four children and live happily. One day, a meteor threatens the city and Thundertooth must use his abilities to save everyone.

**Yi 34B:**
> The story follows Thundertooth, a dinosaur who finds himself transported from prehistoric times to a futuristic city. Initially struggling to adapt and find food, he is taken in by Mayor Eleanor Grace and the citizens of the city. With their help, he establishes a successful toy factory that creates magical widgets, which bring joy to children and adults alike. Thundertooth marries Seraphina, another dinosaur, and they have four children who grow up in this advanced society. One day, the city faces an impending meteor strike, and Thundertooth, with his family and the mayor's support, works to save the city from disaster.

Note: Yi-34B created and answered more questions within each response.

**Mixtral 8X7B:**
> Thundertooth, a talking dinosaur, stumbles upon a futuristic city where he finds acceptance and a new home [2][1]. Initially, he struggles to find food that satisfies his hunger without causing harm to the city's inhabitants. However, with the help of Mayor Grace, they discover a sustainable solution [3]. Thundertooth, inspired by the advanced technology around him, starts a toy factory that becomes a sensation, producing magical widgets adored by children and adults alike [2]. Eventually, he meets Seraphina, and they start a family together [2]. When a massive meteor threatens Earth, Thundertooth steps up to help, collaborating with the city's scientists to find a solution to divert or neutralize the impending catastrophe [1]. In this extraordinary city of advanced technology, Thundertooth becomes a beloved figure and a symbol of unity between the past and the future.

Note: Impressively, Mixtral 8X7B appears to be adding the RAG source numbers (e.g. '[2]') to the text, see the answer to the next question and response by Mixtral 8X7B that includes the source references and also lists the sources:

Q: Who was the main protagonist?

> The main protagonist in this story is Thundertooth. He is depicted as a highly intelligent and resourceful character who has made a significant impact on the futuristic city and its inhabitants. When a massive meteor threatens Earth, Thundertooth takes charge and works with his family and Mayor Grace to find a solution [1][2]. Additionally, Thundertooth is also the founder of a successful toy factory that produces magical, interactive toys using cutting-edge technology [2]. His unique abilities and leadership skills make him the central figure in this narrative.
<br><br>
> Sources:<br>[1] file_name: Thundertooth Part 3.docx, Source 1<br>[2] file_name: Thundertooth Part 2.docx, Source 2