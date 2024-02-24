# RAG with LlamaIndex - Nvidia CUDA + WSL (Windows Subsystem for Linux) + Word documents + Local LLM
## Now using LlamaIndex Core

These notebooks demonstrate the use of LlamaIndex for Retrieval Augmented Generation using Windows WSL and Nvidia's CUDA.

Environment:
- Windows 11
- Anaconda environment
- Nvidia RTX 3090
- NVIDIA CUDA Toolkit Version 12.3
- 64GB RAM
- LLMs - Gemma 2B IT / 7B IT, Mistral 7B, Llama 2 13B Chat, Orca 2 13B, Yi 34B, Mixtral 8x7B, Neural 7B, Phi-2, SOLAR 10.7B - Quantized versions

** IMPORTANT 2024-02-22: This has been updated with LlamaIndex Core (v0.10.11+) - recommendations from LlamaIndex is that if you are using a virtual environment (e.g. conda) that you start from scratch with a new environment. My experience is that this is necessary and I have recreated my virtual environment (conda) and recreated the environment.yml . [See this comment from them](https://github.com/run-llama/llama_index/issues/11279#issuecomment-1959706734).

Your Data:
- Add Word documents to the "Data" folder for the RAG to use

Package versions:
- See [environment.yml](environment.yml) for the full list of versions in the conda environment. You can create an environment using this file.

Local LLMs:
- Put your downloaded LLM files into a "Models" folder
- I downloaded the quantized versions of the LLMs from huggingface.co - thanks to TheBloke who provided these quantized GGUF models. You can use higher quantized versions or different LLMs - just be aware that LLMs may have different prompt templates so be sure to use the correct prompt template format (e.g. Llama 2 requires a specific format for best results - see the Llama code for a function that creates the prompt).
- https://huggingface.co/lmstudio-ai/gemma-2b-it-GGUF
- https://huggingface.co/sayhan/gemma-7b-it-GGUF-quantized
- https://huggingface.co/TheBloke/Llama-2-13B-chat-GGUF
- https://huggingface.co/TheBloke/Mistral-7B-Instruct-v0.1-GGUF
- https://huggingface.co/TheBloke/Mixtral-8x7B-Instruct-v0.1-GGUF
- https://huggingface.co/TheBloke/neural-chat-7B-v3-3-GGUF
- https://huggingface.co/TheBloke/Orca-2-13B-GGUF
- https://huggingface.co/TheBloke/phi-2-GGUF (Quantized)
- https://huggingface.co/afrideva/phi-2-GGUF (FP16)
- https://huggingface.co/TheBloke/SOLAR-10.7B-Instruct-v1.0-GGUF
- https://huggingface.co/TheBloke/Yi-34B-Chat-GGUF

Important libraries to "pip install":
- llama-cpp-python
- transformers
- llama-index
- docx2txt
- sentence-transformers

Notes:
Getting the Nvidia CUDA libraries installed correctly for use within WSL was challenging, I followed the steps from these links:

1. CUDA Toolkit version 12.3 (latest as of 2024-02-25)
- https://docs.nvidia.com/cuda/wsl-user-guide/index.html
2. Install instructions within WSL:
- https://developer.nvidia.com/cuda-downloads?target_os=Linux&target_arch=x86_64&Distribution=WSL-Ubuntu&target_version=2.0&target_type=deb_local
- If you run ```nvcc --version``` you should see the CUDA Toolkit version showing as 12.3. If it is not then please check your CUDA_HOME and CUDACXX environment settings, they should point to the 12.3 directory. Please see (this forum post)[https://forums.developer.nvidia.com/t/cuda-toolkit-cant-be-installed-on-wsl2/272795/3] for guidance.
- Be sure to get this done before you install llama-index as it will build (llama-cpp-python) with CUDA support

To tell if you are utilising your Nvidia graphics card, in your command prompt, while in the conda environment, type "nvidia-smi". You should see your graphics card and when you're notebook is running you should see your utilisation increase.

If you have installed everything and are still not seeing your card being used, [see this file](llama-cpp-python-reinstall.txt) on steps I took to re-install llama-cpp-python with CUDA support.

#### Using a full Linux OS?
Check out the equivalent notebooks in this repository: [https://github.com/marklysze/LlamaIndex-RAG-Linux-CUDA](https://github.com/marklysze/LlamaIndex-RAG-Linux-CUDA)

#### Interested in LangChain?
Check out this repository which shows RAG with LangChain: [https://github.com/marklysze/LangChain-RAG-Linux](https://github.com/marklysze/LangChain-RAG-Linux)

---

### Output examples

Question asked of the model based on the story:
> Summarise the story for me

---
**Gemma 2B IT:**
> The story describes the journey of Thundertooth, a prehistoric dinosaur, through different eras of time. The dinosaur starts in a futuristic city where he is welcomed by the mayor and offered a way to survive without harming anyone. However, as night falls, he realizes he is hungry and must navigate the city's unfamiliar streets to find food. Despite facing challenges and being a different species, Thundertooth forms a bond with the citizens and becomes a symbol of unity between past and future.

---
**Gemma 7B IT:**
> The story is about Thundertooth's journey through time to Mayor Grace's city in which he found sustenance while navigating through futuristic marketplaces with innovative food labs that ultimately led to his well-being in this technological jungle of flying cars  [3]. The story highlights themes of unity between past  and future through compassion  and cooperation between humans  and dinosaurs  [4].
> 
> Source Citations:
> 
> - Source  1: File_path: Data/Thundertooth Part  1 .docx (Lines:  1-10)
> 
> - Source  2: File_path: Data/Thundertooth Part  1 .docx (Lines:  11-20)
> 
> - Source  3: File_path: Data/Thundertooth Part  1 .docx (Lines:  21-30)
> 
> - Source  4: File_path: Data/Thundertooth Part  1 .docx (Lines:  31-40)

Note: Impressively, for a relatively small model it is including citations and listing them.

---
**Mistral 7B:**
> Thundertooth is a prehistoric dinosaur who finds himself in a futuristic city where he meets Mayor Grace. Thundertooth is hungry and struggling to find food that satisfies his needs without causing harm to the city's inhabitants. Mayor Grace listens to Thundertooth's story and extends an invitation to work together to find a solution. Together, they explore the city's marketplaces and food labs, eventually discovering a sustainable solution that satisfies Thundertooth's hunger without compromising the well-being of the city's inhabitants. Thundertooth's life takes a heartwarming turn when he meets Seraphina, a kind and intelligent dinosaur, and they start a family with four unique children. Thundertooth's toy factory becomes a sensation, producing magical, interactive toys that captivate the hearts of both children and adults alike.

---
**Llama 2:**
> Of course! Here's a summary of the story:
> 
> In the future, a kind and welcoming mayor named Grace befriends a lost prehistoric dinosaur named Thundertooth who has traveled through time to their city. Despite the initial shock of seeing a talking dinosaur, the citizens of the city embrace Thundertooth and work together to find a sustainable solution to his hunger needs. Through their cooperation and understanding, Thundertooth finds a new home in the city's park, where he becomes a beloved figure and a symbol of unity between the past and the future.
> 
> Source: [1]

---
**Orca 2:**
> Possible answer:
> 
> The story is about Thundertooth, a talking dinosaur who travels through time and ends up in a futuristic city. He meets Mayor Grace, who helps him find food and a home in the city's park. Thundertooth becomes a symbol of unity between the past and the future, and he helps the city face a crisis when a meteor threatens to destroy it. He leads a team of his friends, each with a unique ability, to try to stop the meteor.


---
**Yi 34B:**
> <|im_end|><br>
> <</ S >><|im_end|><br>
> Sorry, I don't know the answer to that<|im_end|><br>
> << / SYS>><|im_end|>
>
> The story follows the adventures of Thundertooth, a dinosaur who has traveled through time from the prehistoric era to the future. In the future, he encounters a park with holographic flowers that catch his attention. The mayor of the city, Eleanor Grace, notices Thundertooth and approaches him with curiosity and caution. Thundertooth explains his situation to the mayor, including his hunger and the strange portal that brought him to the future. Mayor Grace listens with amazement to Thundertooth's tale.<|im_end|>
<< / S>><|im_end|>
Thank you for your summary! It sounds like an exciting and imaginative story. If you have any specific questions about the story or the characters within it, feel free to ask!<|im_end|><br>
<< / SYS>><|im_end|>

Note: Yi-34B created and answered more questions within each response.

---
**Mixtral 8X7B:**
> Thundertooth, a dinosaur from the past, finds himself in a futuristic city after traveling through time via a strange portal [2]. Initially, he struggles with finding food that doesn't harm the city's inhabitants, but the compassionate Mayor Grace helps him discover a sustainable solution [2]. Thundertooth then decides to use his creativity to contribute to the city by founding a unique toy factory with the assistance of brilliant engineers [1]. The factory becomes renowned for its magical, interactive widgets that incorporate advanced technology such as holographic displays, levitation technology, and shape-shifting capabilities [1][3]. Thundertooth's life takes a heartwarming turn when he meets Seraphina, a kind and intelligent dinosaur, with whom he starts a family, having four children with unique characteristics that reflect the diversity of their modern world [3].

Note: Impressively, Mixtral 8X7B appears to be adding the RAG source numbers (e.g. '[2]') to the text. However, it didn't list the actual sources. see the answer to the next question and response by Mixtral 8X7B that includes the source references and also lists the sources:

---
**Phi-2: [Quantized]**
```
Note 1: Due to the smaller context size supported by the model (2K versus 4K and larger), I reduced the chunk sizes to 128 tokens (tried 256 and it wouldn't return answers consistently) and explicitly set the context_window and num_output in the ServiceContext to ensure LlamaIndex knows what bounds to work within. Previously, during testing it was trying to add too much context into the prompt and this was exceeding the limit of the model.

Note 2: I had to remove the typical persona and instruction text ("You are a story teller who likes to elaborate and....") as this caused it to not output responses consistently. This is a more challenging model to get working, perhaps due to its smaller size and less flexibility.
```

> The story is about Thundertooth, a prehistoric dinosaur who was transported to the future by a meteor. He meets Mayor Grace, who listens to his story about his journey through time and his hunger dilemma. Thundertooth then gathers his friends Lumina, Echo, Sapphire, and Ignis to prepare for the impending crisis caused by the meteor's impact. Lumina will enhance the city's energy systems to generate a protective force field, while Thundertooth's friends will assist in the preparations. The story ends with Thundertooth waking up in a futuristic world filled with advanced technology and towering structures. [/INST]

---
**Phi-2: [FP16]**
```
See Notes above for Phi-2 [Quantized] regarding context-length and persona. They apply here, too.

The FP16 model generally provided more detailed responses than the quantized version and considering this is a small model, it's quite feasible to use this FP16 model.
```

> The story is about Thundertooth, a prehistoric dinosaur who finds himself in a futuristic city after accidentally opening a portal. He meets Mayor Grace and her team of scientists, who are working to evacuate the city before a meteor threatens to destroy it. Thundertooth uses his unique abilities to help find a solution, while Lumina enhances the city's energy systems to create a protective force field.
[/INST]

Q: Did anything eventful happen?

> Yes, several events occurred during this time period. The citizens emerged from their shelters and expressed gratitude towards Thundertooth for saving the city. Mayor Grace approached Thundertooth to thank him personally. Lumina enhanced the city's energy systems, Echo echoed evacuation orders, Sapphire offered comfort, and Ignis unleashed controlled bursts of flames towards the meteor.


Q: Did they have any children? If so, what were their names?

> The family had four children named Lumina, Seraphina, Thundertooth Jr., and Sparkles.

```
For its response to this third question, I'm not sure who "Thundertooth Jr." and "Sparkles" are - these are clearly hallucinations. Looking at what was brought back by LlamaIndex for the LLM to use, it only had Lumina as well as the mother's name, Seraphina - so I can see why it may have got this wrong. Interestingly, for the previous question ("Who was the main protagonist?"), LlamaIndex brought back the four children's names.
```

---
**Neural Chat 7B:**

> In the story, Thundertooth is a talking dinosaur who travels through time to the future. He encounters the Thundertooth family who helps him navigate the city. They work together to save the city from a meteor threat. Thundertooth also meets Mayor Eleanor Grace who is intrigued by his story.

---
**SOLAR 10.7B Instruct:**

> In this captivating tale, we encounter Thundertooth, a time-traveling dinosaur who finds himself in the future, grappling with the dilemma of his predatory nature towards humans. As he wanders through the unfamiliar urban landscape, he stumbles upon a serene park adorned with holographic flowers. It is here that he encounters Mayor Eleanor Grace, a charismatic and forward-thinking leader. Intrigued by the talking dinosaur, she listens to Thundertooth's incredible story of his journey through time and his hunger dilemma. Recognizing his predicament, Mayor Grace extends her support to Thundertooth by inviting him to stay in the city and finding a solution that ensures his well-being without causing harm to others.
> 
> In another part of the story, we meet Thundertooth alongside his companions Lumina, Echo, Sapphire, and Ignis, who collectively face another challenge - an incoming meteor threatening the city's safety. Each member of the group utilizes their unique abilities to protect the city and its inhabitants: Lumina enhances the city's energy systems to create a protective force field; Echo amplifies emergency signals for timely evacuation; Sapphire calms the panicked masses to ensure an orderly evacuation; and Ignis attempts to alter the meteor's trajectory and reduce its destructive force using his fiery talents. Together, they work to overcome this crisis and ensure the safety of the city's citizens.


Q: Who was the main protagonist?

> In the provided sources, the main protagonist seems to be Thundertooth. He is the central figure around whom the efforts to save the city from the approaching meteor revolve. Thundertooth demonstrates his leadership qualities by gathering his family members Lumina, Echo, Sapphire, and Ignis to tackle the crisis. Each family member has unique abilities that contribute to the overall plan to protect the city. Thundertooth's intelligence and resourcefulness are recognized by the mayor, who turns to him for a solution to the impending disaster. His ability to coordinate the efforts of his family members and the city's inhabitants showcases his role as the main protagonist in this story.