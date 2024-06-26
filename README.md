# Inference Endpoints for Large Language Models

Below you'll find the necessary instructions in order to run the provided code.

There are 6 endpoints included and 4 vision-language SoTA models are utilized.


## 1. Requirements
---
1. CUDA compatible GPU 
   1. The more VRAM the better but at least 12GB of VRAM are recommended
2. For LINUX (tested on Ubuntu 20.04)
   1. The system was tested on Nvidia proprietary driver 515 and 525
   2. Make sure Docker is installed on your system. For instructions you can refer to the [official docker guide](https://docs.docker.com/desktop/install/ubuntu/)
   3. Make sure you have the NVIDIA Container Toolking installed. More info and instructions can be found in the [official installation guide](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html#docker)
3. For Windows
   1. Windows 10 (or above) which supports CUDA utilzation with docker (if you wish to run the docker images)
4. Python 3.10.9 was used for all the provided code

One you have docker up and running you can move to cloning the repository.

## 2. Cloning the repository
---
1. Start by cloning the repository by running the following command:
   `git clone https://github.com/stefbil/inference-endpoints-for-llms.git`
   

## 3. Building the docker images
---
In order to build the docker images from scratch you should follow the instructions below:

1. inference-endopoints-for-llms
   1. You should have the following directory structure:
      ```
      inference-endpoints-for-llms
      ├── code
      │   ├── demo.py
      │   ├── extracting_data.py
      │   ├── image_caption.py
      │   ├── main.py
      │   ├── modeling_frcnn.py
      │   ├── pnpv2.py
      │   ├── processing_image.py
      │   ├── requirements.txt
      │   ├── utils.py
      │   ├── vilt_vqa.py
      │   └── visualizing_image.py  
      ├── huggingface (may not exist)
      ├── torch (may not exist)
      ├── dockerfile
      |── LINUX_Start_Contrainer.sh
      ├── LINUX_Stop_Container.sh
      ├── WIN_GPU_Start_Container.bat
      ├── WIN_GPU_Stop_Container.bat
      └── README.md
      ```
     2. The `huggingface` and `torch` directories contain the serving models. If they don't exist, they will be downloaded automatically when you run the docker container.
     3. Build the docker image by running the following command while on the base directory:
         `sudo docker build .`


## 4. Running the docker images
---
1. For LINUX
   1. You can start the docker container by running the `LINUX_Start_Contrainer.sh` script.
   2. There should be a message in the terminal that will display wether the GPU is available or not (the container won't run if there's no GPU available).
   3. Once the container has started, you can move to the `https://localhost:5035/docs` or `https://YourExternalIP:5035/docs` address on your browser and start using the api.
   4. To stop the container run the `LINUX_Stop_Container.sh` script. This script will create a `Dumps` folder and copy all the tests you have run e.g. uploaded photos and questions.
2. For Windows
   1. You can start the container by running the `WIN_GPU_Start_Container.bat` script.
   2. There should be a message in the terminal that will display wether the GPU is available or not (the container won't run if there's no GPU available).
   3. Once the container has started, you can move to the `https://localhost:5035/docs` or `https://YourExternalIP:5035/docs` address on your browser and start using the api.
   4. To stop the container run the `WIN_GPU_Stop_Container.bat` script. This script will create a `Dumps` folder and copy all the tests you have run e.g. uploaded photos and questions.


Further instructions on running the docker images can be found in the [here](DockerInstructions.md).

Disclaimer:
1.  The api serves the models developed in 4 SoTA projects:
 2.  Here's the [code](https://github.com/salesforce/LAVIS/tree/main/projects/pnp-vqa) for the [PNP-VQA paper](https://arxiv.org/abs/2210.08773)
 3.  Here's the [code](https://github.com/huggingface/transformers/tree/main/examples/research_projects/lxmert) for the [LXMERT paper](https://arxiv.org/abs/1908.07490)
 4.  Here's the [ViT_GPT2 model](https://huggingface.co/nlpconnect/vit-gpt2-image-captioning) provided by [NLP Connect](https://github.com/nlpconnect)
 5.  Here's the [BLIP model](https://huggingface.co/Salesforce/blip-vqa-base) from the [paper](https://arxiv.org/abs/2201.12086)
