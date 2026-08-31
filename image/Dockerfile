FROM runpod/worker-comfyui:5.8.5-base

RUN printf '  diffusion_models: models/diffusion_models/\n  text_encoders: models/text_encoders/\n  seedvr2: models/SEEDVR2/\n' >> /comfyui/extra_model_paths.yaml
RUN apt-get update && apt-get install -y --no-install-recommends ffmpeg git && rm -rf /var/lib/apt/lists/*
RUN comfy-node-install \
    https://github.com/kijai/ComfyUI-KJNodes.git \
    https://github.com/ssitu/ComfyUI_UltimateSDUpscale.git \
    https://github.com/numz/ComfyUI-SeedVR2_VideoUpscaler.git
