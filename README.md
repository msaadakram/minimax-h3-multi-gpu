# MiniMax H3 Multi-GPU (Colab/Kaggle + ComfyUI)

This repository provides a ready-to-run notebook for launching **MiniMax H3 video generation** with **ComfyUI** on environments like **Google Colab** and **Kaggle**, with support for running separate ComfyUI instances on multiple GPUs.

## What is included

- `/home/runner/work/minimax-h3-multi-gpu/minimax-h3-multi-gpu/fork-of-minimax-h3-comfyui-orchestrator.ipynb`  
  End-to-end setup and orchestration notebook.

## What the notebook does

1. Installs base system and Python dependencies.
2. Clones ComfyUI into `/tmp/ComfyUI`.
3. Creates model directories.
4. Downloads MiniMax H3 model components from Hugging Face:
   - diffusion model
   - text encoder
   - video VAE
   - audio VAE
5. Installs ComfyUI requirements and ComfyUI Manager.
6. Starts ComfyUI processes for multiple GPUs (separate ports).
7. Installs and runs `cloudflared` to expose ComfyUI via public tunnel URLs.

## Quick start

1. Open `fork-of-minimax-h3-comfyui-orchestrator.ipynb` in Colab or Kaggle.
2. Enable GPU runtime (multi-GPU environment recommended).
3. Run cells top-to-bottom.
4. After startup, check logs from:
   - `/tmp/comfyui_gpu0.log`
   - `/tmp/comfyui_gpu1.log`
5. Use generated Cloudflare tunnel links to access ComfyUI instances.

## Default runtime details

- ComfyUI ports: `8188` (GPU0), `8189` (GPU1)
- Local host: `127.0.0.1`
- Main working directory: `/tmp/ComfyUI`

## Notes

- Model downloads are large; first run can take significant time.
- The notebook relies on external services (Hugging Face + GitHub release assets).
- If ports are already in use, the notebook attempts to kill existing processes before restart.

## Troubleshooting

- If ComfyUI does not start, inspect:
  - `/tmp/comfyui_gpu0.log`
  - `/tmp/comfyui_gpu1.log`
- If tunnel links do not appear, inspect:
  - `/tmp/cloudflared_8188.log`
  - `/tmp/cloudflared_8189.log`
- Re-run the setup and launcher cells after runtime resets.
