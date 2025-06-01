# Exploring IBM Granite LLM Models

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
![Python 3.9+](https://img.shields.io/badge/python-3.9+-blue.svg)
![Framework: Hugging Face Transformers](https://img.shields.io/badge/Framework-🤗%20Transformers-orange.svg)
![Framework: llama-cpp-python](https://img.shields.io/badge/Framework-llama--cpp--python-lightgrey.svg)

This repository contains Jupyter notebooks and experiments focused on exploring IBM's Granite series of Large Language Models (LLMs). It demonstrates how to run these models using two primary methods with a focus on **Named Entity Recognition (NER)** tasks that generate **structured JSON output**.

## 🎯 Overview

The project explores two different approaches to running IBM Granite models:

1. **Hugging Face Transformers Library** - For running original models with 8-bit quantization
2. **llama-cpp-python** - For running GGUF quantized versions optimized for CPU with optional GPU offloading

## ✨ Features

- **Dual Framework Demonstration** - Compare Hugging Face `transformers` vs `llama-cpp-python` implementations
- **Quantization Exploration** - Test various quantization levels from full precision to Q2_K
- **Structured JSON Output** - Focus on reliable, parseable JSON generation for downstream applications
- **NER Task Implementation** - Practical Named Entity Recognition using driver's license text extraction
- **Performance Benchmarking** - Comprehensive inference time measurements and comparisons

## 🤖 Models Explored

### Via Hugging Face Transformers
- `ibm-granite/granite-3.1-2b-instruct`
- `ibm-granite/granite-3.2-2b-instruct`
- `ibm-granite/granite-3.3-2b-instruct` (with 8-bit quantization)

### Via llama-cpp-python (GGUF Format)

**From `bartowski/granite-3.1-2b-instruct-GGUF`:**
- `granite-3.1-2b-instruct-Q8_0.gguf`
- `granite-3.1-2b-instruct-IQ4_XS.gguf`
- `granite-3.1-2b-instruct-Q4_0.gguf`

**From `ibm-granite/granite-3.3-2b-instruct-GGUF`:**
- `granite-3.3-2b-instruct-Q2_K.gguf`
- `granite-3.3-2b-instruct-Q4_K_S.gguf`
- `granite-3.3-2b-instruct-Q8_0.gguf`

## 🎯 Key Task: Named Entity Recognition

The core demonstration involves extracting structured information from driver's license text. Models are prompted to return data in this JSON format:

```json
{
    "address": {
        "license": "B1231241",
        "Address": "X City",
        "Sex": "Male",
        "Weight": "X",
        "Height": "X"
    }
}
```

> **Note:** Actual extracted fields and structure may vary based on the model's interpretation of the prompt and input text.

## 📋 Prerequisites

- **Python 3.9+**
- **pip** (Python package installer)
- **Git**
- **CUDA-enabled GPU** (recommended for optimal performance)
- **NVIDIA drivers and CUDA toolkit** (for GPU acceleration)
- **nvcc** in PATH (required for llama-cpp-python GPU support)

## 🚀 Setup and Installation

### 1. Clone the Repository

```bash
git clone https://github.com/SakibAhmedShuva/Exploring-IBM-Granite-LLM-Models.git
cd Exploring-IBM-Granite-LLM-Models
```

### 2. Create Virtual Environment

```bash
python -m venv .venv

# On Windows
source .venv/Scripts/activate

# On macOS/Linux
source .venv/bin/activate
```

### 3. Install Dependencies

#### For CPU-only Setup:
```bash
pip install -r requirements.txt
```

#### For GPU Support (CUDA):
```bash
# First, ensure nvcc is in your PATH, then:
pip uninstall llama-cpp-python -y
CMAKE_ARGS="-DLLAMA_CUBLAS=on" FORCE_CMAKE=1 pip install llama-cpp-python --no-cache-dir

# Then install other requirements:
pip install -r requirements.txt
```

> **Note:** Check the [llama-cpp-python documentation](https://github.com/abetlen/llama-cpp-python) for OS-specific CUDA installation instructions.

## 📚 Usage

### Starting Jupyter

```bash
jupyter lab
# or
jupyter notebook
```

Models will be downloaded automatically on first run.

### Available Notebooks

#### `ibm_granite.ipynb`
- **Purpose:** Demonstrates IBM Granite models via Hugging Face Transformers
- **Models:** 3.1-2b, 3.2-2b, 3.3-2b instruct variants
- **Features:** 8-bit quantization (`load_in_8bit=True`) for memory efficiency
- **Tasks:** NER with JSON output and inference time measurement

#### `ibm-granite-gguf.ipynb`
- **Purpose:** Explores GGUF quantized versions using llama-cpp-python
- **Models:** 3.1-2b and 3.3-2b instruct variants
- **Quantization Levels:** Q8_0, IQ4_XS, Q4_0, Q2_K, Q4_K_S
- **Tasks:** Same NER task with performance comparisons

## 📊 Key Observations

Running these notebooks will help you observe:

- **Output Quality** - How different models and quantization levels affect JSON extraction accuracy
- **Inference Speed** - Performance trade-offs between model size, quantization, and response time
- **Memory Usage** - Resource efficiency of GGUF and 8-bit quantized models
- **Implementation Differences** - Setup and execution variations between frameworks

## 📝 Requirements File

Create a `requirements.txt` file with these dependencies:

```txt
torch
transformers
accelerate
bitsandbytes
llama-cpp-python
jupyterlab
ipywidgets
```

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🤝 Contributing

Contributions are welcome! Here's how you can help:

1. **Fork** the repository
2. **Create** a new branch (`git checkout -b feature/YourFeature`)
3. **Make** your changes
4. **Commit** your changes (`git commit -m 'Add some feature'`)
5. **Push** to the branch (`git push origin feature/YourFeature`)
6. **Open** a Pull Request

Please ensure your code follows reasonable coding standards and include clear descriptions of your changes.

---

This repository serves as a practical guide and testbed for anyone looking to integrate IBM Granite models into their applications, especially when structured output and performance are key considerations.
