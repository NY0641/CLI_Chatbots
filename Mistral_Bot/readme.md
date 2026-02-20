# 🤖 Mistral Conversational CLI Chatbot

---

## 📌 Overview

This project implements a **production-structured conversational chatbot** powered by the **Mistral-7B-Instruct large language model**.

The system demonstrates how modern open-source LLMs can be safely deployed in a conversational interface with:

- Secure authentication practices  
- Automatic hardware detection  
- Memory-safe conversation handling  
- Quantized model loading for efficiency  
- Structured prompt management using chat templates  

The notebook functions as both:

- ✅ A working conversational CLI chatbot  
- ✅ A reference architecture for LLM deployment workflows  

---

## 🎯 Business Objective

The goal of this project is to showcase how open-source LLMs can be deployed in a **controlled, efficient, and production-oriented way**, rather than as a simple demo notebook.

It demonstrates:

- How conversational memory can be managed safely  
- How large models can run on limited GPU resources  
- How authentication and model access should be handled securely  
- How inference pipelines can be structured for reproducibility  

This architecture can be extended into:

- Customer support assistants  
- Internal knowledge bots  
- Developer copilots  
- Enterprise conversational interfaces  

---

## 🧠 Model Details

| Attribute | Value |
|----------|-------|
| **Model** | Mistral-7B-Instruct v0.1 |
| **Type** | Instruction-tuned large language model |
| **Provider** | Mistral AI via HuggingFace |
| **Context Length** | ~8K tokens |
| **Interface** | Text-generation pipeline with chat template |

The model is loaded in **4-bit quantized mode using BitsAndBytes**, allowing it to run on consumer GPUs.

---

## 💻 Hardware Requirements

### ✅ Recommended
- GPU with **≥ 8GB VRAM**
- CUDA-enabled environment
- Google Colab GPU runtime works well

### ⚠️ Minimum
- CPU execution supported  
- Expect significantly slower responses  

Quantization reduces memory usage from **~28GB → ~6–8GB**.

---

## 🔐 Authentication & Security

The notebook uses a **production-safe authentication flow**.

Priority order:

1. Environment variable (`HF_TOKEN`)
2. Google Colab Secrets
3. Interactive secure prompt

This prevents accidental credential leakage in shared notebooks and follows best practices for gated model access.

---

## ⚙️ System Architecture

The chatbot follows a structured runtime pipeline:

### 1️⃣ Environment Setup
Installs required libraries and dependencies.

### 2️⃣ Secure Authentication Layer
Ensures gated models can be accessed safely.

### 3️⃣ Runtime Hardware Detection
Automatically determines:

- Whether GPU is available  
- Whether VRAM is sufficient  
- Optimal tensor precision  

This prevents runtime crashes and ensures optimal performance.

### 4️⃣ Safe Model Loader
Wraps model initialization with:

- Timeout protection  
- Error propagation  
- Predictable failure handling  

This avoids notebook hangs when resources are insufficient.

### 5️⃣ Quantized Model Initialization
The model loads with:

- 4-bit quantization  
- Automatic device placement  
- Precision based on hardware  

This enables large models to run in constrained environments.

---

## 🧩 Conversational Memory Management

A common issue with LLM chat systems is **unbounded memory growth**, which can cause:

- Context overflow errors  
- Slow inference  
- Excessive token usage  

This project implements a **token-based sliding window strategy**:

- Each conversation is converted to tokens  
- If token count exceeds threshold, oldest messages are removed  
- The system prompt is always preserved  

This ensures:

- Stable inference  
- Predictable performance  
- Memory-safe conversation handling  

---

## 💬 Prompt Construction

Instead of manually concatenating text, the system uses:

```python
tokenizer.apply_chat_template()
