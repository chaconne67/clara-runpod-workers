FROM runpod/worker-comfyui:5.8.5-base

ARG COMFYUI_COMMIT=95d755cd8107a72258d452b5d3657273d571f07d
RUN cd /comfyui \
 && git fetch --depth 1 origin ${COMFYUI_COMMIT} \
 && git checkout ${COMFYUI_COMMIT} \
 && uv pip install --python /opt/venv/bin/python -r requirements.txt

RUN printf '  diffusion_models: models/diffusion_models/\n  text_encoders: models/text_encoders/\n  seedvr2: models/SEEDVR2/\n' >> /comfyui/extra_model_paths.yaml
RUN apt-get update && apt-get install -y --no-install-recommends ffmpeg git && rm -rf /var/lib/apt/lists/*
RUN comfy-node-install \
    https://github.com/kijai/ComfyUI-KJNodes.git \
    https://github.com/ssitu/ComfyUI_UltimateSDUpscale.git \
    https://github.com/numz/ComfyUI-SeedVR2_VideoUpscaler.git \
    https://github.com/ltdrdata/ComfyUI-Impact-Pack.git \
    https://github.com/ltdrdata/ComfyUI-Impact-Subpack.git
