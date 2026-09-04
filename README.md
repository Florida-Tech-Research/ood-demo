# ood-demo

A notebook that generates images from text prompts on a GPU, run from a browser on
AI.Panther through Open OnDemand. It is the hands-on portion of the September 14th workshop,
and it will keep working afterward if you want to come back to it.

You need an AI.Panther account. If you are off campus, connect to the VPN first, otherwise
ood.fit.edu will not resolve.

## Getting the notebook

Log in at <https://ood.fit.edu> and open **Clusters > AI.Panther Shell Access**, which gives
you a login shell in the browser. Clone the repo there:

```
git clone https://github.com/Florida-Tech-Research/ood-demo.git
```

It lands in your home directory, which is where Jupyter will start, so you will not need to
move it.

## Starting a Jupyter session

Go to **Interactive Apps > Jupyter** and fill in the form. The defaults are close, but set
the partition and make sure you are asking for a GPU:

| Field | Value |
|---|---|
| Partition | vdi-short |
| Hours / Minutes | 0 / 45 |
| CPUs | 8 |
| Memory (GB) | 16 |
| GPUs | 1 |
| Modules to load | leave blank |
| Working Directory | leave blank |

Jupyter sessions run on the vgpu nodes, so you get a 12 GB slice of an L40S.

Click **Connect to Jupyter** when the session starts, open `ood-demo/demo.ipynb`, and work
down from the top. The first cell installs a kernel. When it finishes, switch to the
`OOD Demo` kernel using the picker in the top right. If you forget, the next cell fails on an
import error, which is generally how people find out they are still on the default kernel.

The same notebook runs unchanged under **Interactive Apps > Code Server** if you would rather
work in VS Code.

## What is already staged

Nothing in the notebook downloads anything while it runs. The environment and model weights
are under `/shared/workshops/ood_jupyter`:

| Path | Contents |
|---|---|
| `venv/` | PyTorch, diffusers, transformers, ipykernel |
| `ooddemo.py` | Loads the model and runs generation, safety checker always on |
| `models/sd-turbo/` | SD-Turbo weights in fp16, about 2.5 GB |
| `models/safety-checker/` | Stable Diffusion safety checker |
| `samples/` | Reference images generated during staging |

Generation takes about 0.08 seconds per image and peaks around 3.9 GB of the 12 GB of VRAM,
so there is plenty of room left over.

## Capacity

There are 24 GPU slices across vgpu01, vgpu02 and vgpu03. Delete your session from
**My Interactive Sessions** when you are done so someone else can have it.
