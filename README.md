# ComfyUI_WorkFlow

The purpose of this repo is to store the utilized workflows, 
document their corresponding usage methods, 
and note down any precautions or points of attention.

## How to use ComfyUI & Node Manager & install Custom-Nodes
[ComfyUI](https://github.com/comfyanonymous/ComfyUI) is 
the most powerful and modular diffusion model GUI and backend.

[ComfyUI-Example](https://comfyanonymous.github.io/ComfyUI_examples/): This ui will let you design and 
execute advanced stable diffusion pipelines using a graph/nodes/flowchart based interface. 
For some workflow examples and see what ComfyUI can do you can check out:

[ComfyUI-Manager](https://github.com/ltdrdata/ComfyUI-Manager) is a tool for
us to manage(install&uninstall) the nodes and checkpoints.

Once you have installed ComyUI, you can easily use it by running `python main.py`. 
If you want to run it on a local area network (LAN), simply add the `--listen` option. 
It is important to place each checkpoint in the correct location.
For instance, the model file `flux.1-dev.safetensors` should reside in the `diffusion_models` directory instead of the `checkpoints` folder."

Since some custom nodes are not available in the Node Manager, 
you can manually add them by cloning the repository into the `custom-nodes` directory and then restarting ComfyUI.

## Base Model
The term "base model" refers to open-source foundation models, 
such as SDXL, SD3, Flux and SD3.5.

### 1.SDXL & SD3 & SD3.5
`SD_workflow_ComfyUI.json`

The official guidelines about [`SD3-medium`](https://comfyanonymous.github.io/ComfyUI_examples/sd3/README_old.html) and [`SD3.5-large`](https://comfyanonymous.github.io/ComfyUI_examples/sd3/#sd35).
It is crucial to download the correct checkpoints and place them in the appropriate folders.
Because the text encoders are numerous and intricate; especially for T5-XXL, which requires excessive memory that exceeds the available GPU memory.

Note: If you want to use `t5xxl_fp16`, it is recommended that you have more than 32GB  RAM.
### 2.Flux
The official guidelines about [`flux`](https://comfyanonymous.github.io/ComfyUI_examples/flux/).

`flux-dev_workflow.json`: the [`flux.1-dev`](https://huggingface.co/black-forest-labs/FLUX.1-dev/tree/main) model 
is capable of generating excellent images.

`flux-schnell_workflow.json`: support the [`flux.1-schnell`](https://huggingface.co/black-forest-labs/FLUX.1-schnell)

`flux1-dev-fp8_workflow.json` While it is feasible to run the flux.1-dev model on an RTX 4090, 
we do not recommend using this workflow due to the resulting output quality is 
significantly lower than expected.

## In-Context LoRA
`In-Context-LoRA.json` We can follow the [official guidelines](https://github.com/ali-vilab/In-Context-LoRA?tab=readme-ov-file) 
to generate images with in-context information. 
Additionally, there is a wide variety of [community-contributed](https://github.com/ali-vilab/In-Context-LoRA?tab=readme-ov-file#community-creations-using-ic-lora) 
LoRA models available.

## IPAdapter
### 1.SD3.5L_IPAdapter

`SD3.5L_IPAdapter.json` provide the workflow refer to [custom nodes repo](https://github.com/Slickytail/ComfyUI-InstantX-IPAdapter-SD3), 
This model is released by researchers from [InstantX Team](https://huggingface.co/InstantX).

### 2.Flux.1_IPAdapter

There are three different workflows that support distinct roles.

`Flux_IPAdapter.json`

`Flux_IPAdapter_start-end-percent.json`

`Flux_multi-IPAdapter.json`

There are two important points to note:
* The model `google/siglip-so400m-patch14-384` is used as the image encoder. 
However, the default code may attempt to load this model from an incorrect path due to web-related issues. 
Therefore, the code has been modified as follows:
```python
# - model = InstantXFluxIPAdapterModel(image_encoder_path=clip_vision, ip_ckpt=ipadapter, device=provider, num_tokens=128)

clip_path = os.path.join(folder_paths.models_dir, "clip", "siglip-so400m-patch14-384")
model = InstantXFluxIPAdapterModel(image_encoder_path=clip_path, ip_ckpt=ipadapter, device=provider, num_tokens=128)
```
* Use the model `flux1-dev.safetensors` instead of `flux1-dev-fp8_e4m3fn.safetensors`.