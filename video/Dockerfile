FROM runpod/worker-comfyui:5.8.5-base

RUN printf '  text_encoders: models/text_encoders/\n  latent_upscale_models: models/latent_upscale_models/\n  diffusion_models: models/diffusion_models/\n  rife: models/rife/\n' >> /comfyui/extra_model_paths.yaml
RUN apt-get update && apt-get install -y --no-install-recommends ffmpeg wget git && rm -rf /var/lib/apt/lists/*
RUN comfy-node-install \
    https://github.com/Kosinkadink/ComfyUI-VideoHelperSuite.git \
    https://github.com/kijai/ComfyUI-KJNodes.git \
    https://github.com/kijai/ComfyUI-PromptRelay.git \
    https://github.com/TenStrip/10S-Comfy-nodes.git \
    https://github.com/rgthree/rgthree-comfy.git \
    https://github.com/crystian/ComfyUI-Crystools.git \
    https://github.com/yolain/ComfyUI-Easy-Use.git \
    https://github.com/GACLove/ComfyUI-VFI.git \
    https://github.com/Lightricks/ComfyUI-LTXVideo.git
RUN mkdir -p /comfyui/models/rife && /opt/venv/bin/python /comfyui/custom_nodes/ComfyUI-VFI/rife/download_rife.py /comfyui/models/rife && test -f /comfyui/models/rife/flownet.pkl
RUN python3 - <<'PY'
path = "/handler.py"
src = open(path).read()
anchor = "        for node_id, node_output in outputs.items():\n"
assert anchor in src, "handler.py layout changed"
src = src.replace(anchor, anchor + ('            if node_output.get("gifs"):\n' '                node_output.setdefault("images", []).extend(node_output.pop("gifs"))\n'), 1)
open(path, "w").write(src)
PY
