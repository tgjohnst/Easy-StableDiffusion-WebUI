# StableDiffusion AI image generation web-app for GPU clouds
## What is this?
[Stable Diffusion](https://stability.ai/blog/stable-diffusion-public-release) is an incredibly powerful AI model that specializes in art generation - it's an incredibly powerful way to generate and refine images and art using text and image prompts. This repository contains code for running a simple yet powerful Gradio web application that lets you use the power of Stable Diffusion on commodity cloud GPU services without writing any code. The notebook linked below can simply be run from top to bottom, no other accounts or data required, to get a working WebUI for Stable Diffusion with support for face correction (GFPGAN) and superresolution upscaling (ESRGAN).

![Screenshot of the webUI running](sd_webgui_runpod_screenshot.jpg)

## How do I run it?
Code is contained in [the linked iPython Notebook](stablediffusion_runpod_adapted_webgui.ipynb) which can be run directly in JupyterLab locally, on the cloud, or on RunPod or similar cloud providers. If you're working on a cloud provider that has a Jupyterlab interface, simply upload this notebook to Jupyterlab and run it. The notebook comes preconfigured for runpod but can be trivially adapted to any other environment by changing a couple variables. 

### Dependencies
All of these dependencies should come preinstalled when running on commodity GPU services (such as RunPod, LambdaLabs, Colab, SageMaker) or using pre-built deep learning VMs in cloud providers (such as AWS/GCP/Azure). You'll need to have the following available when the notebook runs:
- jupyterlab
- CUDA
- conda/miniconda

### RunPod setup
If running on RunPod, I built this based on the RunPod Pytorch container. That said, this notebook does not make use of the built-in preinstalled pytorch or conda environment as version/dependency incompatibilities between the preinstalled packages and the ones needed by the pipeline make it much easier to start fresh. Start a pod with your GPU of choice (I recommend minimum 16GB VRAM, the more the better) using the Pytorch container. It's your choice whether you want to save money by using a spot instance, but be aware that interruptions are common unless you reserve a dedicated GPU. Click `Connect` and open up the Jupyterlab interface. Upload the notebook (.ipynb) file in this repository and run through it cell by cell. Voila!

## Why use a public cloud provider?
If you don't have a powerful GPU at home, it's significantly cheaper to rent time on public GPUs than to buy one. Even if you do have a top-of-the-line consumer GPU (e.g. a 3090), image generation can be slow and is limited to one small image at a time due to the VRAM that consumer cards have. 

Running StableDiffusion on a public cloud provider is also generally cheaper than DALL-E and similar managed services. DALL-E costs $15 for 115 images, and while relatively easy to use is not very customizable. With this notebook and an appropriate GPU, you can generate that many images in a few minutes for less than $0.50 and have far more control over your art.

I chose [RunPod](https://www.runpod.io) because it's the cheapest way I've found to get GPU time on powerful GPUs, often costing less than 1/3 of comparable cloud providers. 

## Persistence?
This notebook is designed to create a persistent conda environment and model files in the `/workspace/` directory, which persists across stopping and starting pods so you don't have to redownload and reinstall everything every time you start a new runtime. It can easily be modified to use any similar persistent storage in other services (e.g. a google drive mount in Google Colab).

## Tips
Ensure you're on a GPU with the appropriate VRAM for what you're trying to generate. GPUs with 16GB or less VRAM will probably only be able to generate a single 512x512 image at a time. Larger GPUs like the A100 are recommended but definitely more expensive.

## Credits
This notebook is based off a similar colab notebook by Altryne and the amazing Stable Diffusion webui. Go support them!
- https://github.com/altryne/sd-webui-colab
- https://github.com/hlky/stable-diffusion
