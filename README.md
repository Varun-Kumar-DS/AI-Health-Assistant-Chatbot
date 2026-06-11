# AI-Health-Assistant-Chatbot

# Gradio Health Chatbot (phi-1.5)

> An early exploration into deploying open-source LLMs locally — a Gradio interface wrapping Microsoft's **phi-1.5** for general Q&A, framed as a lightweight health assistant.

[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?logo=python&logoColor=white)]()
[![Transformers](https://img.shields.io/badge/🤗-Transformers-FFD21E)]()
[![Gradio](https://img.shields.io/badge/Gradio-FF7C00?logo=gradio&logoColor=white)]()
[![Model](https://img.shields.io/badge/Model-phi--1.5-512BD4)]()

---

## 📌 Overview

This was my first hands-on project deploying a transformer-based chatbot end-to-end — loading a Hugging Face model, building a generation pipeline, and serving it through a Gradio UI in Google Colab. It directly informed the design decisions behind my flagship project, [**BERU**](https://github.com/varun-kumar-ds/BERU), where I moved to a production-grade stack (Flask + Groq + LLaMA 3.3 70B, deployed on Render).

## 🧱 Stack

- **Model:** `microsoft/phi-1_5` (1.3B params)
- **Framework:** Hugging Face `transformers`
- **UI:** Gradio
- **Runtime:** Google Colab (GPU)

## 🚀 Run

Open the notebook in Colab and run cells top-to-bottom. The Gradio interface launches with a public share link.

```python
llm_model = AutoModelForCausalLM.from_pretrained("microsoft/phi-1_5", trust_remote_code=True)
interface = gr.Interface(fn=chatbot, inputs="text", outputs="text")
interface.launch()
```

## 📚 What I Learned

- How tokenizers, attention masks, and `generate()` parameters (`top_k`, `top_p`, `max_length`) shape model output
- Why **small open-source models struggle with instruction following** vs. larger hosted models — a key motivation for moving BERU to a 70B model via Groq
- Trade-offs between self-hosting an open model (cost, control) and using an API (latency, quality, simplicity)
- Gradio is excellent for prototyping but isn't production deployment — a Flask + frontend split scales better

## 🔭 Known Limitations & Next Steps

This project is preserved as a learning artefact. Issues identified during code review (and addressed in BERU):

- Tokenizer should be loaded once at startup, not per request
- System prompt was defined but never injected into the generation call
- End-of-sequence handling should use the tokenizer's EOS token, not string matching
- No multi-turn conversation memory

## ➡️ Where this led

This project → **[BERU](https://github.com/varun-kumar-ds/BERU)**, a deployed LLM assistant on my [portfolio](https://varun-kumar-ds.github.io) that fixes every limitation above and serves real recruiter traffic.

## 📬 Contact

**Varun Kumar** · [Portfolio](https://varun-kumar-ds.github.io) · MSc Data Science & AI, University of Liverpool
