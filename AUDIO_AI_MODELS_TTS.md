# Audio AI Models & Text-to-Speech Systems
**Last Updated:** 2026-01-10
**Research Session:** Deep Knowledge Gathering

---

## 🎙️ Text-to-Speech Models Comparison

| Model | Parameters | Languages | Zero-Shot Cloning | License | Special Features |
|-------|-----------|-----------|-------------------|---------|------------------|
| **Audio Flamingo 3** | 7B | Multi-domain | ✅ | Non-Commercial | 10min audio, 3 modalities |
| **Chatterbox-Multilingual** | 500M | 23+ | ✅ | MIT | Neural watermarking |
| **Chatterbox-Turbo** | 350M | English | ✅ | MIT | Paralinguistic tags |
| **F5-TTS** | - | Multi (CN+EN) | ✅ | MIT/CC-BY-NC | ConvNeXt V2, Sway sampling |
| **Kokoro** | 82M | 9 languages | ✅ | Apache-2.0 | StyleTTS 2 based |

---

## 🔊 Audio Flamingo Series (NVIDIA)

### Repository
**URL:** https://github.com/NVIDIA/audio-flamingo
**License:** MIT (code) / NVIDIA OneWay Noncommercial (checkpoints)

### Model Evolution

#### Audio Flamingo 3 (NeurIPS 2025 Spotlight) ⭐
**Architecture:** 7B language model + LLaVA multimodal integration

**Capabilities:**
- **Three Audio Modalities:** Sound, Music, Speech
- **Input Length:** Up to 10 minutes
- **Training Data:** ~50M audio-text pairs

**Performance:**
- Outperforms Qwen-Audio, SALMONN, Gemini variants
- SOTA on multiple audio understanding benchmarks

**Components:**
```
┌──────────────────────────┐
│  AF-Whisper (Encoder)    │  ← Unified audio encoder
│  Whisper-based           │
└────────────┬─────────────┘
             ↓
┌──────────────────────────┐
│  Qwen-2.5 (7B)           │  ← Language model backbone
│  LLaVA architecture      │
└────────────┬─────────────┘
             ↓
┌──────────────────────────┐
│  Multimodal Understanding│
│  Sound/Music/Speech      │
└──────────────────────────┘
```

#### Audio Flamingo 2 (ICML 2025)
**Architecture:** 3B language model
**Capabilities:**
- Audio understanding up to 5 minutes
- Training: 10M audio-text pairs
- Focus datasets: AudioSkills, LongAudio

**Training Strategy:**
- 3-stage progressive training
- Qwen-2.5-3B backbone
- Improved temporal understanding

#### Music Flamingo (arXiv)
**Specialization:** Music analysis and understanding

**Advanced Features:**
- Chain-of-thought reasoning
- Reinforcement learning integration
- Musical element analysis:
  - Harmony structures
  - Song structure (verse/chorus/bridge)
  - Timbre characteristics
  - Cultural context recognition

#### Audio Flamingo 1 (ICML 2024)
**Architecture:** 1.3B language model (OPT-IML based)

**Capabilities:**
- Few-shot learning for audio tasks
- Multi-turn dialogue about audio content
- Training: 5.9M audio-text pairs

### Technical Stack
- **Framework:** PyTorch
- **Audio Encoder:** AF-Whisper (unified Whisper variant)
- **LLM Backbones:** Qwen-2.5 (AF2/AF3), OPT-IML (AF1)

### Available Resources
- HuggingFace model checkpoints (all versions)
- Gradio demos for interactive testing
- Training datasets: AudioSkills-XL, LongAudio-XL, AF-Chat, AF-Think
- Separate GitHub branches per model version

### Citation & Papers
- AF3: NeurIPS 2025 (Spotlight presentation)
- AF2: ICML 2025
- Music Flamingo: arXiv preprint
- AF1: ICML 2024

---

## 🗣️ Chatterbox Series (Resemble AI)

### Repository
**URL:** https://github.com/resemble-ai/chatterbox
**Stars:** 21.1k ⭐
**License:** MIT

### Model Variants

#### Chatterbox-Turbo (350M) 🚀
**Release:** Newest addition (efficiency-focused)

**Key Innovation: Paralinguistic Tags**
```
Example:
"Hello [laugh] I can't believe this [chuckle] amazing feature [cough]"

Supported tags:
- [laugh]
- [chuckle]
- [cough]
- [throat_clear]
- [sigh]
- Additional emotional markers
```

**Technical Achievement:**
- Reduces mel-decoder generation: 10 steps → 1 step
- Maintains audio quality despite massive speedup
- Real-time inference capable

#### Chatterbox-Multilingual (500M) 🌍
**Languages:** 23+ supported

**Capabilities:**
- Zero-shot voice cloning
- Cross-language voice transfer
- Language ID specification
- Localization-ready

**Use Cases:**
- Global content localization
- Multilingual virtual assistants
- International audiobook production

#### Original Chatterbox (500M)
**Language:** English only

**Advanced Features:**
- CFG (Classifier-Free Guidance) tuning
- Exaggeration parameter for creative synthesis
- High-fidelity speech quality

### Technical Implementation

**Installation:**
```bash
pip install chatterbox-tts
```

**Basic Usage:**
```python
from chatterbox import ChatterboxTTS

# Load model
model = ChatterboxTTS.from_pretrained("resemble-ai/chatterbox-turbo")

# Generate speech with voice cloning
output = model.generate(
    text="Your text here [laugh]",
    audio_prompt_path="reference_voice.wav",
    cfg_weight=1.0,      # Guidance strength
    exaggeration=1.2     # Emphasis control
)

# Save output
import torchaudio
torchaudio.save("output.wav", output, 24000)
```

**Environment:**
- Python 3.11
- Debian 11 OS
- PyTorch-based
- Dependencies in `pyproject.toml`

### Unique Features

#### Neural Watermarking (Perth Watermarker)
**Purpose:** Responsible AI tracking and provenance

**Characteristics:**
- Imperceptible to human hearing
- Survives MP3 compression
- Persists through audio editing
- Enables content tracing

**Ethical Implementation:**
- All generated audio automatically watermarked
- Helps combat deepfakes and misinformation
- Transparency in AI-generated content

### Tunable Parameters
- `cfg_weight`: Guidance scale (0.0-2.0)
- `exaggeration`: Emphasis intensity (0.5-2.0)
- `language_id`: Target language code (multilingual model)
- `reference_audio`: Voice cloning source

### Integration Examples
- Gradio web UI (`example_tts.py`)
- Voice conversion (`example_vc.py`)
- Batch processing scripts

---

## 🎵 F5-TTS

### Repository
**URL:** https://github.com/SWivid/F5-TTS
**License:** MIT (code) / CC-BY-NC (models)

### Architecture
**Foundation:** Diffusion transformer with ConvNeXt V2 blocks

**Key Innovation: Sway Sampling**
- Inference-time optimization strategy
- Improves quality without retraining
- Faster convergence during generation

### Model Variants

| Model | Type | Training Data | Languages |
|-------|------|---------------|-----------|
| **F5-TTS Base** | Standard | Emilia dataset | CN + EN |
| **E2 TTS** | Flat-UNet Transformer | Paper reproduction | Multi |

### Capabilities
1. **Basic TTS** - Text-to-speech with chunk inference
2. **Multi-Style** - Multiple speaking styles per voice
3. **Multi-Speaker** - Voice diversity within single model
4. **Voice Chat** - Powered by Qwen2.5-3B-Instruct
5. **Custom Inference** - Extended language support

### Performance Metrics
**Hardware:** L20 GPU
**Configuration:** 16 NFE (Network Forward Evaluation) steps

**Results:**
- RTF (Real-Time Factor): ~0.04
- Average Latency: 253ms (across 26 test samples)
- Mode: Client-server architecture

### Installation Options

#### Pip Install (Inference Only)
```bash
pip install f5-tts
```

#### Full Install (Training + Fine-tuning)
```bash
git clone https://github.com/SWivid/F5-TTS
cd F5-TTS
pip install -r requirements.txt
```

#### Docker Deployment
```bash
docker pull ghcr.io/swivid/f5-tts:latest
docker run --gpus all -p 7860:7860 ghcr.io/swivid/f5-tts
```

### System Requirements
- Python 3.10+
- PyTorch (device-specific):
  - NVIDIA: CUDA toolkit
  - AMD: ROCm
  - Intel: XPU drivers
  - Apple Silicon: MPS backend
- FFmpeg

### Usage Methods

#### Gradio Web Interface
```bash
f5-tts_infer-gradio
```

#### Command Line Interface
```bash
f5-tts_infer-cli --config inference_config.toml
```

#### Fine-tuning Interface
```bash
f5-tts_finetune-gradio
```

### Technical Highlights
- **Chunk Inference:** Handles long-form text efficiently
- **Voice Embedding:** Compact voice representation
- **Streaming Support:** Real-time generation capable
- **Configuration Files:** TOML-based settings

### Training Dataset
**Emilia:** Large-scale multilingual speech corpus
- Explains CC-BY-NC licensing for pretrained models
- Code remains MIT licensed for custom training

---

## 🌸 Kokoro TTS

### Repository
**URL:** https://github.com/hexgrad/kokoro
**License:** Apache 2.0

### Overview
**Kokoro** is an "open-weight TTS model with 82 million parameters" delivering quality comparable to much larger models while being faster and more cost-efficient.

### Model Specifications
- **Parameters:** 82M (lightweight compared to alternatives)
- **Architecture:** StyleTTS 2 based
- **Sample Rate:** 24,000 Hz
- **License:** Apache 2.0 (fully open)

### Language Support

| Code | Language | Notes |
|------|----------|-------|
| `a` | American English | Default |
| `b` | British English | UK accent |
| `e` | Spanish (Español) | Castilian |
| `f` | French (Français) | |
| `h` | Hindi (हिन्दी) | |
| `i` | Italian (Italiano) | |
| `j` | Japanese (日本語) | |
| `p` | Portuguese (Português) | Brazilian variant |
| `z` | Chinese (中文) | Mandarin |

### Installation

#### Linux
```bash
pip install kokoro>=0.9.4 soundfile
apt-get install espeak-ng
```

#### Windows
```bash
pip install kokoro>=0.9.4 soundfile
# Download espeak-ng .msi installer from GitHub releases
```

#### macOS (with GPU)
```bash
export PYTORCH_ENABLE_MPS_FALLBACK=1
pip install kokoro>=0.9.4 soundfile
brew install espeak-ng
```

### Usage Example
```python
from kokoro import KPipeline

# Initialize pipeline
pipeline = KPipeline(lang_code='a')  # American English

# Generate audio
text = "Hello world, this is Kokoro TTS!"
generator = pipeline(text, voice='af_heart', speed=1.0)

# Process streaming output
for i, (graphemes, phonemes, audio) in enumerate(generator):
    # graphemes: text representation
    # phonemes: pronunciation units
    # audio: numpy array of waveform

    # Save audio chunk
    import soundfile as sf
    sf.write(f'output_{i}.wav', audio, 24000)
```

### Advanced Features

#### Voice Selection
- Multiple voice profiles (e.g., 'af_heart')
- Custom voice tensor loading
- Voice style customization

#### Speed Control
```python
pipeline(text, voice='af_heart', speed=0.8)  # Slower
pipeline(text, voice='af_heart', speed=1.2)  # Faster
```

#### Debugging Output
- Grapheme-to-phoneme conversion visible
- Phoneme stream for pronunciation analysis
- Text splitting pattern customization

### Technical Stack
- **Languages:** JavaScript (51.5%), Python (47.0%)
- **G2P Library:** `misaki` (grapheme-to-phoneme conversion)
- **Distribution:** PyPI package
- **Testing:** Included test suite

### Key Advantages
1. **Lightweight:** 82M params vs 500M-7B in alternatives
2. **Fast Inference:** Efficient generation
3. **Cost-Effective:** Lower compute requirements
4. **Open License:** Apache 2.0, no restrictions
5. **Multi-Language:** 9 languages out of the box

---

## 📊 Model Selection Guide

### By Use Case

#### Real-Time Applications
**→ Kokoro or Chatterbox-Turbo**
- Lowest latency
- Efficient resource usage
- Good quality for interactive apps

#### Multilingual Products
**→ Chatterbox-Multilingual or Kokoro**
- Broad language coverage
- Zero-shot voice cloning
- Consistent quality across languages

#### Maximum Audio Understanding
**→ Audio Flamingo 3**
- Long-form audio (10min)
- Multi-domain (sound/music/speech)
- Advanced reasoning about audio content

#### Creative Speech Synthesis
**→ Chatterbox-Turbo or Original Chatterbox**
- Paralinguistic tags (laugh, cough, etc.)
- Exaggeration controls
- Emotional expression

#### Music Analysis
**→ Music Flamingo**
- Specialized music understanding
- Harmony and structure analysis
- Cultural context recognition

#### Production Quality TTS
**→ F5-TTS or Chatterbox**
- High fidelity output
- Voice cloning capability
- Watermarking for provenance

---

## 🔧 Technical Considerations

### VRAM Requirements
```
Audio Flamingo 3 (7B):   ~16-24GB
Audio Flamingo 2 (3B):   ~8-12GB
Chatterbox-Multilingual: ~4-6GB
Chatterbox-Turbo:        ~3-4GB
F5-TTS:                  ~2-4GB
Kokoro:                  ~1-2GB
```

### Inference Speed (RTF = Real-Time Factor)
```
Kokoro:            < 0.1 RTF  (fastest)
Chatterbox-Turbo:  ~0.05 RTF
F5-TTS:            ~0.04 RTF
Chatterbox-Multi:  ~0.15 RTF
Audio Flamingo:    Variable (understanding task)
```

**RTF < 1.0 = Faster than real-time**

### Licensing Summary

| Model | Code License | Model License | Commercial Use |
|-------|-------------|---------------|----------------|
| Audio Flamingo | MIT | Non-Commercial | ❌ Research only |
| Chatterbox | MIT | MIT | ✅ Full commercial |
| F5-TTS | MIT | CC-BY-NC | ❌ Non-commercial |
| Kokoro | Apache-2.0 | Apache-2.0 | ✅ Full commercial |

---

## 🎯 Integration Examples

### Voice Assistant Pipeline
```python
# 1. Speech Recognition
from whisper import load_model
stt_model = load_model("base")
text = stt_model.transcribe("user_query.wav")

# 2. LLM Processing
from openai import OpenAI
client = OpenAI()
response = client.chat.completions.create(
    model="gpt-4",
    messages=[{"role": "user", "content": text}]
)

# 3. TTS Response
from chatterbox import ChatterboxTTS
tts = ChatterboxTTS.from_pretrained("resemble-ai/chatterbox-turbo")
audio = tts.generate(
    text=response.choices[0].message.content + " [chuckle]",
    audio_prompt_path="assistant_voice.wav"
)
```

### Multilingual Content Localization
```python
from kokoro import KPipeline

# English source
en_pipeline = KPipeline(lang_code='a')
en_audio = en_pipeline("Welcome to our service", voice='af_heart')

# Spanish translation
es_pipeline = KPipeline(lang_code='e')
es_audio = es_pipeline("Bienvenido a nuestro servicio", voice='af_heart')

# Japanese translation
ja_pipeline = KPipeline(lang_code='j')
ja_audio = ja_pipeline("私たちのサービスへようこそ", voice='af_heart')
```

### Audio Understanding Application
```python
from audio_flamingo import AudioFlamingoModel

# Load model
model = AudioFlamingoModel.from_pretrained("nvidia/audio-flamingo-3")

# Analyze audio
result = model.generate(
    audio_path="podcast_episode.wav",
    prompt="Summarize the main topics discussed in this podcast and identify the speakers."
)

print(result)  # AI-generated analysis
```

---

## 🔬 Research & Development

### Watermarking Technology
**Perth Watermarker (Chatterbox):**
- Embeds imperceptible signatures
- Survives lossy compression
- Enables AI content tracking
- Combats deepfake misuse

### Future Directions
- **Longer Context:** Audio Flamingo pushing toward 30+ minute understanding
- **Emotion Transfer:** More nuanced emotional expression in TTS
- **Streaming Optimization:** Sub-100ms latency for real-time apps
- **Cross-Modal Learning:** Joint audio-visual-text models
- **Few-Shot Adaptation:** Rapid voice customization with minimal data

---

## Tags
`#tts` `#text-to-speech` `#audio-ai` `#voice-cloning` `#audio-understanding` `#multilingual` `#zero-shot` `#nvidia` `#resemble-ai` `#kokoro` `#f5-tts` `#audio-flamingo` `#chatterbox` `#speech-synthesis`
