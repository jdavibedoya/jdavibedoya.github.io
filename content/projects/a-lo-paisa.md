---
title: "A lo Paisa"
description: "Voice-to-Voice Pipeline for Antioquian Spanish."
summary: "Voice-to-Voice Pipeline for Antioquian Spanish."
date: 2026-06-26
tags: ["AI Engineering", "Python", "Speech-to-Text", "LLM", "RAG", "Text-to-Speech", "Voice Cloning", "PyTorch", "Hugging Face", "Docker"] 
cover:
    image: "https://github.com/jdavibedoya/a-lo-paisa/raw/refs/heads/main/assets/architecture_diagram.webp"
    alt: "Architecture Workflow - Illustrated with ChatGPT"
    caption: "Architecture Workflow - Illustrated with ChatGPT"
    relative: false
---

### ⛰️🫓 Project Overview
End-to-end voice pipeline that transforms speech audio into Paisa Spanish (Antioquia, Colombia) using a cloned voice.

This project emphasizes **AI Engineering**, showcasing how to orchestrate AI models into a production-ready Python package. The architecture leverages open-weight models for audio processing (STT and Zero-Shot TTS), free tiers for LLM/embedding APIs and serverless deployment on Hugging Face Spaces, `uv` for deterministic dependency resolution and `Docker` for containerization. This approach differs from the first projects in my portfolio and the [master's thesis](https://zenodo.org/records/4091394) developed during my internship at Voctro Labs, which focused on model architecture and training in Jupyter/Colab.

### 🎧 Examples
| Dials&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Input | Output |
| :--- | :--- | :--- |
| *Idioma:* `español`<br>*Exageración:* `2`<br>*Registro:* `urbano` | [⬇️ Download](https://github.com/jdavibedoya/a-lo-paisa/releases/download/examples/spanish_input.wav)<br><small>"Hoy es un día tranquilo en la montaña con algo de lluvia y un cielo gris me gusta correr temprano y escuchar música"</small> | [⬇️ Download](https://github.com/jdavibedoya/a-lo-paisa/releases/download/examples/spanish_output.wav)<br><small>"Hoy está el día como tranquilito por acá en la montaña, con una agüita y el cielo medio gris. A mí me gusta, pues, correr bien tempranito y escuchar música."</small> |
| *Idioma:* `inglés`<br>*Exageración:* `2`<br>*Registro:* `montañero` | [⬇️ Download](https://github.com/jdavibedoya/a-lo-paisa/releases/download/examples/english_input.wav)<br><small>"She can scoop these things into three red bags and we will go meet her Wednesday at the train station."</small> | [⬇️ Download](https://github.com/jdavibedoya/a-lo-paisa/releases/download/examples/english_output.wav)<br><small>"Ella puede meter esas cositas en tres bolsas rojas y nos pillamos con ella el miércoles en la estación del tren, ¿sí o qué?"</small> |

---

### 🚀 [Hugging Face Space](https://huggingface.co/spaces/jdavibedoya/a-lo-paisa)
<iframe
	src="https://jdavibedoya-a-lo-paisa.hf.space"
	frameborder="0"
	width="100%"
	height="800"
></iframe>

### 🎚️ Dials
- *Idioma de entrada:* `español` | `inglés` | `otro`
- *Exageración:* `1` (suave) | `2` (cotidiano) | `3` (recargado)
- *Registro:* `urbano` (parlache) | `montañero` (rural / tradicional)

### ⚙️ Pipeline Stages
1. **Input Voice**
2. **STT (Speech-to-Text):** Automatically detects the language if set to `otro`.
3. **(Translation):** Handled by an LLM (triggered only if the *Idioma de entrada* dial is `inglés` or `otro`).
4. **Paisa Rewriting:** An LLM rewrites the text, enriched by **semantic RAG** against a curated glossary. This stage is modulated by the *Exageración* and *Registro* dials.
5. **TTS (Text-to-Speech):** Synthesizes the text with a cloned voice. The *Exageración* dial influences the model's prosodic variance and acoustic expressiveness.
6. **Output Voice**

---

### 🧠 Models
| Stage | Model |
|-------|-------|
| **STT** | faster-whisper `small`, int8 |
| **Translation / Rewriting** | Gemini `2.5-flash` |
| **Embeddings (RAG)** | `gemini-embedding-001`, dim 768 |
| **TTS** | Chatterbox V3 (Multilingual) + es-MX Language Pack |

### 🔗 [GitHub Repository](https://github.com/jdavibedoya/a-lo-paisa) 
Visit the repository to view the source code and detailed architectural decisions.