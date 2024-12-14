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
such as SDXL, SD3, Flux, and SD3.5.

### 1.SDXL & SD3 & SD3.5
`SD_workflow_ComfyUI.json`

### 2.Flux
`flux-dev_workflow.json`: the [`flux.1-dev`](https://huggingface.co/black-forest-labs/FLUX.1-dev/tree/main) model 
is capable of generating excellent images.

`flux-schnell_workflow.json`: support the [`flux.1-schnell](https://huggingface.co/black-forest-labs/FLUX.1-schnell)

`flux1-dev-fp8_workflow.json` While it is feasible to run the flux.1-dev model on an RTX 4090, 
we do not recommend using this workflow due to the resulting output quality is 
significantly lower than expected.

## In-Context LoRA
`In-Context-LoRA.json` We can follow the [official guidelines](https://github.com/ali-vilab/In-Context-LoRA?tab=readme-ov-file) 
to generate images with in-context information. 
Additionally, there is a wide variety of [community-contributed](https://github.com/ali-vilab/In-Context-LoRA?tab=readme-ov-file#community-creations-using-ic-lora) 
LoRA models available.

## SD3.5L_IPAdapter
`SD3.5L_IPAdapter.json` provide the workflow refer to [custom nodes repo](https://github.com/Slickytail/ComfyUI-InstantX-IPAdapter-SD3), 
This model is released by researchers from [InstantX Team](https://huggingface.co/InstantX).
