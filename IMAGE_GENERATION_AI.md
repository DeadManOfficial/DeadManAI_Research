# Image Generation AI Models
**Last Updated:** 2026-01-10
**Research Session:** Deep Knowledge Gathering

---

## 🎨 FLUX.1 - Black Forest Labs

### Repository
**URL:** https://github.com/black-forest-labs/flux
**Documentation:** docs.bfl.ai
**Stars:** 25k ⭐
**Contributors:** 28+
**License:** Apache-2.0 (code), Mixed (models)

---

## 📋 Model Portfolio

| Model | Type | License | Primary Use Case |
|-------|------|---------|-----------------|
| FLUX.1 [schnell] | Text-to-Image | Apache-2.0 ✅ | Fast generation, commercial OK |
| FLUX.1 [dev] | Text-to-Image | Non-Commercial | High quality, dev/research |
| FLUX.1 Fill [dev] | In/Out-painting | Non-Commercial | Image completion/editing |
| FLUX.1 Canny [dev] | Structural Control | Non-Commercial | Edge-based conditioning |
| FLUX.1 Depth [dev] | Structural Control | Non-Commercial | Depth-based conditioning |
| FLUX.1 Redux [dev] | Image Variation | Non-Commercial | Style transfer/variations |
| FLUX.1 Kontext [dev] | Image Editing | Non-Commercial | Context-aware editing |

---

## 🚀 Core Capabilities

### 1. Text-to-Image Generation
**Model:** FLUX.1 [schnell] or [dev]

```python
from flux import FluxModel

model = FluxModel.from_pretrained("flux.1-schnell")
image = model.generate(
    prompt="A serene Japanese garden at sunset, cherry blossoms falling",
    width=1024,
    height=1024,
    steps=4  # schnell is optimized for few steps
)
image.save("output.png")
```

**Performance:**
- schnell: 4 steps, ~2 seconds
- dev: 20-50 steps, higher quality

### 2. In/Out-Painting
**Model:** FLUX.1 Fill [dev]

**Capabilities:**
- **Inpainting:** Fill masked regions
- **Outpainting:** Extend image boundaries
- Context-aware completion

**Use Cases:**
- Remove unwanted objects
- Extend backgrounds
- Complete partial images
- Fix composition issues

### 3. Structural Conditioning

#### Canny Edge Control
**Model:** FLUX.1 Canny [dev]

**Process:**
```
Original Image → Edge Detection (Canny) → Text Prompt → New Image with same structure
```

**Applications:**
- Preserve composition while changing style
- Architectural visualization
- Product design variations
- Sketch-to-image

#### Depth Map Control
**Model:** FLUX.1 Depth [dev]

**Process:**
```
Original Image → Depth Estimation → Text Prompt → New Image with same spatial layout
```

**Applications:**
- 3D scene relighting
- Material changes preserving geometry
- Environmental variations
- Interior design visualization

### 4. Image Variation
**Model:** FLUX.1 Redux [dev]

**Capabilities:**
- Generate variations of existing images
- Style transfer
- Concept exploration
- A/B testing visual designs

### 5. Image Editing
**Model:** FLUX.1 Kontext [dev]

**Context-Aware Editing:**
- Understands scene semantics
- Preserves coherence
- Intelligent object manipulation

---

## 🛠️ Installation & Setup

### Basic Installation
```bash
git clone https://github.com/black-forest-labs/flux
cd flux
python3.10 -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
pip install -e ".[all]"
```

### System Requirements
- **Python:** 3.10+
- **GPU:** CUDA-capable NVIDIA GPU (8GB+ VRAM recommended)
- **Storage:** 15-30GB for model weights
- **OS:** Linux, Windows, macOS (with MPS)

### TensorRT Acceleration (NVIDIA)
```bash
# Using NVIDIA PyTorch container with enroot
enroot import docker://nvcr.io/nvidia/pytorch:24.07-py3
enroot create --name pytorch nvidia+pytorch+24.07-py3.sqsh
enroot start --rw --mount /path/to/flux:/workspace pytorch
```

---

## 🔑 Commercial Licensing

### Open-Source Model: schnell ✅
- **License:** Apache-2.0
- **Commercial Use:** Fully permitted
- **Attribution:** Required
- **Modifications:** Allowed
- **Distribution:** Allowed

### Non-Commercial Models: [dev] variants ❌
- **License:** Non-Commercial FLUX.1 License
- **Personal Use:** Allowed
- **Research:** Allowed
- **Commercial Use:** Requires licensing

**To obtain commercial license:**
- Visit: bfl.ai/pricing/licensing
- Contact Black Forest Labs sales team
- Licensing options for production deployment

---

## 📊 Usage Tracking

### Built-in Telemetry
```bash
# Enable usage tracking (optional)
python inference.py --prompt "..." --track_usage
```

**Purpose:**
- API consumption monitoring
- Model usage analytics
- Performance metrics

**Privacy:**
- Opt-in via `--track_usage` flag
- Can be disabled for air-gapped environments

---

## 🌐 API Access

### Hosted API
**Endpoint:** api.githubcopilot.com

**Available Models:**
- All FLUX.1 open-weight models
- Proprietary Pro-tier models
- Optimized inference infrastructure

**Benefits:**
- No local GPU required
- Auto-scaling
- Managed infrastructure
- Latest model updates

**Authentication:**
- API key required
- Usage-based pricing

---

## 🎯 Model Selection Guide

### Choose FLUX.1 [schnell] When:
✅ Speed is critical (real-time apps)
✅ Commercial deployment needed
✅ Cost-sensitive projects
✅ Good quality sufficient (not ultra-high fidelity)

**Ideal For:**
- Web applications
- Mobile apps
- Chatbot integrations
- Rapid prototyping

### Choose FLUX.1 [dev] When:
✅ Maximum quality needed
✅ Research/development work
✅ Non-commercial projects
✅ Fine-tuning and customization

**Ideal For:**
- Art generation
- Creative workflows
- Academic research
- Professional portfolios (non-commercial)

### Choose FLUX.1 Fill [dev] When:
✅ Editing existing images
✅ Extending compositions
✅ Removing objects
✅ Professional retouching

**Ideal For:**
- Photo editing workflows
- Design iteration
- Content moderation (object removal)
- Image restoration

### Choose FLUX.1 Canny/Depth [dev] When:
✅ Preserving structure critical
✅ Style transfer needs
✅ Architectural visualization
✅ Product design variations

**Ideal For:**
- E-commerce (product variations)
- Architecture firms
- Game asset generation
- Concept art workflows

### Choose FLUX.1 Redux [dev] When:
✅ Variation generation needed
✅ Style exploration
✅ A/B testing visuals
✅ Iterative design process

**Ideal For:**
- Marketing teams
- Brand exploration
- Creative agencies
- Design systems development

### Choose FLUX.1 Kontext [dev] When:
✅ Semantic understanding required
✅ Complex editing tasks
✅ Context preservation critical
✅ Professional editing workflow

**Ideal For:**
- Professional photographers
- Digital artists
- Content creators
- Post-production studios

---

## 🔧 Technical Specifications

### Architecture
- **Foundation:** Diffusion Transformer (DiT)
- **Training:** Multi-stage progressive training
- **Conditioning:** Cross-attention text guidance
- **Sampling:** Advanced noise scheduling

### Performance Benchmarks
```
Model: FLUX.1 [schnell]
Resolution: 1024x1024
Steps: 4
Time: ~2 seconds (RTX 4090)
Quality: High

Model: FLUX.1 [dev]
Resolution: 1024x1024
Steps: 50
Time: ~15 seconds (RTX 4090)
Quality: Ultra-high
```

### VRAM Requirements
```
512x512:   4GB+ VRAM
1024x1024: 8GB+ VRAM
2048x2048: 16GB+ VRAM
4096x4096: 24GB+ VRAM (with optimizations)
```

### Optimizations Available
- **Mixed Precision:** FP16/BF16 for memory efficiency
- **xFormers:** Memory-efficient attention
- **Flash Attention:** Faster inference
- **Model Offloading:** CPU offload for large models
- **TensorRT:** NVIDIA acceleration

---

## 💡 Integration Examples

### Web Application (FastAPI)
```python
from fastapi import FastAPI, File, UploadFile
from flux import FluxModel
import io
from PIL import Image

app = FastAPI()
model = FluxModel.from_pretrained("flux.1-schnell")

@app.post("/generate")
async def generate_image(prompt: str, width: int = 1024, height: int = 1024):
    image = model.generate(prompt=prompt, width=width, height=height)

    # Convert to bytes
    img_byte_arr = io.BytesIO()
    image.save(img_byte_arr, format='PNG')
    img_byte_arr.seek(0)

    return Response(content=img_byte_arr.getvalue(), media_type="image/png")
```

### Discord Bot
```python
import discord
from discord.ext import commands
from flux import FluxModel

bot = commands.Bot(command_prefix='!')
model = FluxModel.from_pretrained("flux.1-schnell")

@bot.command()
async def imagine(ctx, *, prompt: str):
    await ctx.send("Generating image...")
    image = model.generate(prompt=prompt, width=1024, height=1024)

    # Save and send
    image.save("output.png")
    await ctx.send(file=discord.File("output.png"))

bot.run('YOUR_BOT_TOKEN')
```

### Batch Processing Pipeline
```python
from flux import FluxModel
from pathlib import Path
import json

model = FluxModel.from_pretrained("flux.1-schnell")

# Load prompts
with open('prompts.json') as f:
    prompts = json.load(f)

# Batch generate
output_dir = Path('outputs')
output_dir.mkdir(exist_ok=True)

for i, prompt in enumerate(prompts):
    image = model.generate(prompt=prompt['text'], steps=4)
    image.save(output_dir / f"{i:04d}_{prompt['id']}.png")
    print(f"Generated {i+1}/{len(prompts)}")
```

---

## 🎨 Prompt Engineering for FLUX

### Best Practices

#### 1. Be Specific
```
❌ "A cat"
✅ "A fluffy orange tabby cat with green eyes, sitting on a windowsill, soft morning light, photorealistic"
```

#### 2. Include Style Modifiers
```
Style keywords:
- photorealistic, hyperrealistic, cinematic
- oil painting, watercolor, digital art
- minimalist, maximalist, surreal
- vintage, modern, futuristic
```

#### 3. Describe Lighting
```
Lighting terms:
- golden hour, blue hour, harsh midday sun
- soft diffused light, dramatic shadows
- studio lighting, natural light
- backlit, rim light, volumetric lighting
```

#### 4. Specify Composition
```
Composition:
- close-up, medium shot, wide shot
- aerial view, bird's eye view, worm's eye view
- rule of thirds, centered, symmetrical
- shallow depth of field, deep focus
```

#### 5. Add Quality Boosters
```
Quality modifiers:
- highly detailed, intricate details
- 8k resolution, ultra HD
- professional photography
- award-winning
```

### Example Prompts

**Photography Style:**
```
"Portrait of an elderly craftsman in his workshop, weathered hands holding handmade tools, warm tungsten lighting, shallow depth of field, 85mm lens, Kodak Portra 400 film aesthetic, highly detailed, professional photography"
```

**Illustration Style:**
```
"Whimsical forest scene with bioluminescent mushrooms and fireflies, soft pastel colors, children's book illustration style, watercolor and ink, magical atmosphere, trending on ArtStation"
```

**Product Visualization:**
```
"Modern wireless headphones floating on white background, studio lighting setup with soft shadows, product photography, clean and minimal, high-end tech aesthetic, 8k resolution"
```

---

## 🔍 Comparison with Competitors

| Feature | FLUX.1 | Stable Diffusion 3 | DALL-E 3 | Midjourney v6 |
|---------|--------|-------------------|----------|---------------|
| **Open Source** | Partial ✅ | ✅ | ❌ | ❌ |
| **Commercial (Free)** | schnell only | ✅ | API only | ❌ |
| **Speed (schnell)** | Excellent | Good | Good | Slow |
| **Quality (dev)** | Excellent | Excellent | Excellent | Excellent |
| **Control Tools** | Extensive | Moderate | Limited | Moderate |
| **Local Deployment** | ✅ | ✅ | ❌ | ❌ |
| **API Available** | ✅ | ✅ | ✅ | ❌ |

---

## 📚 Resources & Community

### Official Resources
- **Documentation:** docs.bfl.ai
- **GitHub:** github.com/black-forest-labs/flux
- **Model Weights:** Hugging Face Hub
- **API Docs:** API reference at docs site

### Community Resources
- **Discord:** Black Forest Labs community server
- **Reddit:** r/StableDiffusion (FLUX discussions)
- **Twitter:** @bflml (official updates)

### Learning Materials
- Prompt engineering guides
- Model comparison benchmarks
- Integration tutorials
- Best practices documentation

---

## 🚧 Known Limitations

1. **Model Size:** Large download (15-30GB depending on variant)
2. **VRAM Requirements:** High for maximum quality/resolution
3. **Licensing Complexity:** Different licenses per model variant
4. **Commercial Use:** Most models require separate licensing
5. **Fine-tuning:** Limited public documentation (as of Jan 2026)

---

## 🔮 Future Roadmap

### Expected Developments
- Additional control models (pose, segmentation)
- Smaller distilled variants for mobile
- Video generation capabilities
- 3D asset generation
- Improved fine-tuning tools

### Community Requests
- More open-source model variants
- Clearer commercial licensing
- LoRA training support
- Multi-language prompt support

---

## Tags
`#flux` `#image-generation` `#text-to-image` `#black-forest-labs` `#diffusion` `#ai-art` `#commercial` `#open-source` `#inpainting` `#structural-control` `#canny` `#depth` `#image-editing`
