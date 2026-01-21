# Video Generation AI Models & Tools
**Last Updated:** 2026-01-10
**Research Session:** Deep Knowledge Gathering

---

## Overview
Comprehensive analysis of state-of-the-art video generation models, from enterprise-grade DiT architectures to open-source content automation tools.

---

## 🎬 Enterprise-Grade Models

### HunyuanVideo (Tencent)
**Repository:** https://github.com/Tencent-Hunyuan/HunyuanVideo
**Model Size:** 13B+ parameters (largest open-source video model)
**License:** Open-source

#### Capabilities
- Text-to-video generation at 720p (720×1280, 129 frames)
- Image-to-video conversion (HunyuanVideo-I2V variant)
- Professional-grade quality surpassing Runway Gen-3, Luma 1.6

#### Performance Metrics
- **Text Alignment:** 61.8%
- **Motion Quality:** 66.5%
- **Visual Quality:** 95.7%

#### Technical Architecture
```
┌─────────────────────────────────────┐
│  3D VAE (Video Compression)         │
│  - Temporal: 4x compression         │
│  - Spatial: 8x compression          │
│  - Channel: 16x compression         │
└─────────────────────────────────────┘
           ↓
┌─────────────────────────────────────┐
│  MLLM Text Encoder                  │
│  (Multimodal Large Language Model)  │
└─────────────────────────────────────┘
           ↓
┌─────────────────────────────────────┐
│  Dual→Single Stream Architecture    │
│  - Independent video/text tokens    │
│  - Multimodal fusion layer          │
└─────────────────────────────────────┘
           ↓
┌─────────────────────────────────────┐
│  Prompt Rewriting (Hunyuan-Large)   │
│  - Normal mode                      │
│  - Master mode (advanced)           │
└─────────────────────────────────────┘
```

#### Hardware Requirements
- **Minimum:** 60GB GPU (720×1280) or 45GB (544×960)
- **Recommended:** 80GB GPU for optimal quality
- **Platform:** NVIDIA CUDA (11.8/12.4)

#### Quick Start
```bash
# Environment setup
conda create -n HunyuanVideo python==3.10.9
conda activate HunyuanVideo

# Basic inference
python3 sample_video.py --video-size 720 1280 \
  --prompt "A cat walks on the grass"

# Web UI
python3 gradio_server.py --flow-reverse
```

#### Optimization Options
- **Multi-GPU Parallel:** xDiT integration (2-8 GPUs)
- **FP8 Quantization:** ~10GB memory reduction
- **CPU Offloading:** Single-GPU inference support

#### Community Integration
- Hugging Face Diffusers support
- ComfyUI nodes available
- GGUF quantization implementations
- Penguin Video Benchmark for evaluation

---

### LTX-Video (Lightricks)
**Repository:** https://github.com/Lightricks/LTX-Video
**License:** Apache-2.0 / OpenRail-M (commercial)

#### Core Specifications
- **DiT-based** synchronized audio-video generation
- **Native 4K resolution** at up to 50 FPS
- **Single-pass** audio+video generation

#### Model Variants

| Model | Size | Use Case | VRAM |
|-------|------|----------|------|
| ltxv-13b-0.9.8-dev | 13B | Highest quality | High |
| ltxv-13b-0.9.8-distilled | 13B | Faster iteration | Medium |
| ltxv-2b-0.9.8-distilled | 2B | Lightweight/rapid | Low |
| FP8 variants | Quantized | Reduced VRAM | Lowest |

#### Generation Modes
1. **Image-to-Video:** Single image conditioning
2. **Multi-Keyframe Animation:** Multiple conditioning frames
3. **Video Extension:** Forward/backward temporal expansion
4. **Video-to-Video:** Style transfer and transformation

#### Installation
```bash
git clone https://github.com/Lightricks/LTX-Video.git
cd LTX-Video
python -m venv env
source env/bin/activate
python -m pip install -e .[inference]
```

#### Usage Example
```bash
python inference.py \
  --prompt "A cinematic shot of waves crashing" \
  --conditioning_media_paths input.jpg \
  --conditioning_start_frames 0 \
  --height 720 --width 1280 \
  --num_frames 121 \
  --seed 42 \
  --pipeline_config configs/ltxv-13b-0.9.8-distilled.yaml
```

#### Integration Platforms
- **ComfyUI:** Recommended workflow interface (ComfyUI-LTXVideo)
- **HuggingFace Diffusers:** Official library support
- **LTX-Studio:** Online platform (image-to-video, 13B models)
- **Fal.ai / Replicate:** Cloud inference

#### Requirements
- Python 3.10.5+
- CUDA 12.2+ (PyTorch ≥2.1.2)
- macOS via MPS (PyTorch 2.3.0+)

#### Recent Updates (July 2025)
- Distilled models v0.9.8 → 60-second video generation
- New control models: depth, pose, canny edge detection
- Improved prompt understanding and detail generation

---

### LTX-2 (Lightricks)
**Repository:** https://github.com/Lightricks/LTX-2
**Innovation:** First DiT-based audio-video foundation model

#### Advanced Capabilities
- **Camera Control LoRAs:**
  - Dolly movements (in/out)
  - Jib movements (up/down)
  - Static camera shots

- **Image Control (IC-LoRAs):**
  - Canny edge detection
  - Depth map conditioning
  - Pose detection
  - Detail enhancement

- **Core Functions:**
  - Text-to-video & image-to-video
  - Video-to-video transformations
  - Keyframe interpolation

#### Model Checkpoints
```
ltx-2-19b-dev.safetensors           # Full precision 19B
ltx-2-19b-dev-fp8.safetensors       # Quantized 19B
ltx-2-19b-distilled.safetensors     # Optimized for speed
ltx-2-19b-distilled-fp8.safetensors # Speed + memory efficient
```

**Supporting Components:**
- Spatial/temporal upscalers
- Gemma 3 text encoder
- Camera/IC-LoRA modules

#### Pipeline Options

1. **TI2VidTwoStagesPipeline** ⭐ RECOMMENDED
   - Production-ready
   - Includes 2x spatial upsampling

2. **TI2VidOneStagePipeline**
   - Single-stage for rapid prototyping

3. **DistilledPipeline**
   - 8 predefined noise schedules
   - Optimized for speed

4. **ICLoraPipeline**
   - Image/video conditioning

5. **KeyframeInterpolationPipeline**
   - Smooth keyframe transitions

#### Installation
```bash
# Using uv dependency manager
git clone <repo>
cd LTX-2
uv sync --frozen
source .venv/bin/activate  # or .venv\Scripts\activate on Windows
```

#### Performance Optimization
```python
# Recommended settings for speed
- Use DistilledPipeline
- Stage 1: 8 steps
- Stage 2: 4 steps
- Enable FP8 quantization
- Install xFormers or Flash Attention 3
- Reduce steps: 40 → 20-30 (with gradient estimation)
```

#### Architecture (Monorepo)
```
ltx-core/       # Model implementation
ltx-pipelines/  # Generation workflows
ltx-trainer/    # Fine-tuning tools (LoRA, full model)
```

---

## 🤖 Content Automation Tools

### MoneyPrinter
**Repository:** https://github.com/FujiwaraChoki/MoneyPrinter
**Stars:** 12.4k ⭐
**License:** MIT
**Status:** Not accepting PRs

#### Purpose
Automated YouTube Shorts creation from simple topic prompts using MoviePy.

#### Tech Stack
- **Python:** 75.4% (core processing)
- **HTML:** 14.8% (UI)
- **JavaScript:** 8.6% (frontend)
- **Dockerfile:** 1.2% (containerization)

#### Features
- Automated video generation from text prompts
- TikTok integration (requires session ID auth)
- Frontend + Backend architecture
- ImageMagick integration for image processing

#### Installation Considerations
- Docker/Docker Compose support
- Correct ImageMagick path configuration critical
- Known `playsound` dependency issues (documented)

#### Project Stats
- 1.6k forks
- 207 commits
- 25 contributors
- Active Discord community

#### Environment Setup
- Requires `.env` configuration
- `requirements.txt` for Python deps
- WebView runtime needed

---

### MoneyPrinter-Enhanced
**Repository:** https://github.com/Troptrop/MoneyPrinter-Enhanced
**Status:** ❌ 404 - Repository not found or private

---

## 📊 Comparison Matrix

| Model | Size | Speed | Quality | Audio | Open Source | Commercial |
|-------|------|-------|---------|-------|-------------|------------|
| HunyuanVideo | 13B+ | Slow | Highest | ❌ | ✅ | ✅ |
| LTX-Video 13B | 13B | Medium | High | ✅ | ✅ | ✅ |
| LTX-Video 2B | 2B | Fast | Good | ✅ | ✅ | ✅ |
| LTX-2 | 19B | Medium | Highest | ✅ | ✅ | ✅ |
| MoneyPrinter | N/A | Fast | Basic | ❌ | ✅ | ✅ |

---

## 🎯 Use Case Recommendations

### Professional Video Production
**→ HunyuanVideo or LTX-2**
- Highest quality outputs
- Advanced control features
- Suitable for commercial projects

### Rapid Prototyping
**→ LTX-Video 2B Distilled**
- Fast iteration cycles
- Lower VRAM requirements
- Good quality for previews

### Content Automation
**→ MoneyPrinter**
- Automated YouTube Shorts
- Minimal configuration
- Template-based generation

### Audio-Video Sync Required
**→ LTX-Video or LTX-2**
- Native audio generation
- Synchronized output

---

## 🔬 Technical Considerations

### VRAM Requirements Summary
```
HunyuanVideo:  45-80GB
LTX-2 19B:     ~60GB (40GB with FP8)
LTX-Video 13B: ~50GB (35GB with FP8)
LTX-Video 2B:  ~20GB
MoneyPrinter:  Minimal (CPU-based MoviePy)
```

### Platform Support
- **Linux:** All models (best support)
- **Windows:** All (with CUDA toolkit)
- **macOS:** LTX-Video series (MPS backend), MoneyPrinter

---

## 📚 Additional Resources

### Benchmarking
- Penguin Video Benchmark (HunyuanVideo)
- Community comparisons on Papers with Code

### Community Hubs
- ComfyUI node repositories
- HuggingFace model cards
- Discord servers (MoneyPrinter, Lightricks)

---

## Tags
`#video-generation` `#ai-models` `#dit-architecture` `#text-to-video` `#automation` `#content-creation` `#youtube-shorts` `#professional-video` `#open-source`
