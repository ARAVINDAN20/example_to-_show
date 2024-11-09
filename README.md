# Rachel HR Bot - Advanced Interview Preparation Assistant
![Rachel HR Bot Logo](https://github.com/user-attachments/assets/fc5e1b56-9794-440e-b6ef-286ef199a2e8)

## Overview

Rachel HR Bot is a cutting-edge AI-powered interview preparation assistant that leverages NVIDIA's advanced AI technologies and OpenWebUI for a comprehensive interview preparation experience. Developed for the NVIDIA and LlamaIndex Developer Contest, this project combines state-of-the-art language models with robust security features and efficient processing capabilities.

## 🌟 Key Features

- **Advanced AI-Powered Interviews**
  - Utilizing NVIDIA's Nemotron-70B model for human-like interactions
  - Real-time response generation with TensorRT-LLM optimization
  - Context-aware question generation based on resume analysis

- **Comprehensive Security**
  - NeMo Guardrails integration for content safety
  - Professional tone maintenance
  - Ethical AI guidelines compliance

- **Smart Document Processing**
  - Resume analysis using NeMo Curator
  - Technical skill extraction
  - Domain-specific question generation

- **Performance Optimization**
  - GPU acceleration with NVIDIA TensorRT-LLM
  - Efficient batch processing
  - Low-latency response generation

- **Interactive User Interface**
  - OpenWebUI integration for seamless experience
  - Real-time feedback system
  - Progress tracking
  - Interview simulation environment

## 🔧 Technical Architecture

```
+------------------------+     +----------------------+     +-------------------------+
|     User Interface     |     |    Core Engine      |     |    NVIDIA Services     |
|     (OpenWebUI)        | <-> |   (Python/Flask)    | <-> |  (NIM/TensorRT-LLM)   |
+------------------------+     +----------------------+     +-------------------------+
          ↑                            ↑                             ↑
          |                            |                             |
          v                            v                             v
+------------------------+     +----------------------+     +-------------------------+
|   Document Processor   |     |  Security Layer     |     |    Knowledge Base      |
| (NeMo Curator/Reader) |     | (NeMo Guardrails)   |     |   (LlamaIndex/NeMo)   |
+------------------------+     +----------------------+     +-------------------------+
```

## 📋 Requirements

- Python 3.11+
- NVIDIA GPU with CUDA support
- Docker (optional)
- 16GB+ RAM recommended
- 50GB+ disk space

## 🚀 Installation

### Method 1: Direct Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/rachel-hr-bot.git
cd rachel-hr-bot

# Create and activate virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Install NVIDIA components
pip install nvidia-pytriton
pip install nvidia-tensorrt
pip install nemo-toolkit[all]
pip install llama-index
```

### Method 2: Docker Installation

```bash
# Pull and run with GPU support
docker run -d --gpus all \
  -p 3000:8080 \
  -v rachel-data:/app/data \
  -e NVIDIA_API_KEY=your_key \
  --name rachel-hr-bot \
  ghcr.io/yourusername/rachel-hr-bot:latest
```

## 🔨 Core Components Integration

### 1. NVIDIA NeMo Guardrails Setup

```python
from nemo_guardrails import RailsConfig, Guard

class InterviewGuard:
    def __init__(self):
        self.config = RailsConfig.from_content("""
            define rail interview_safety:
                - maintain professional tone
                - ensure technical accuracy
                - avoid discriminatory content
                - provide constructive feedback
        """)
        self.guard = Guard(self.config)
```

### 2. NVIDIA NIM Integration

```python
from nvidia import nim

class ResponseGenerator:
    def __init__(self, api_key):
        self.client = nim.Client(
            base_url="https://api.nvidia.com/v1/nim",
            api_key=api_key
        )

    async def generate_response(self, prompt):
        return await self.client.generate(
            model="nvidia/llama-3.1-nemotron-70b-instruct",
            prompt=prompt,
            max_tokens=1024
        )
```

### 3. TensorRT-LLM Optimization

```python
import tensorrt_llm as trt_llm

class InferenceOptimizer:
    def __init__(self):
        self.engine = trt_llm.Engine(
            model="nvidia/llama-3.1-nemotron-70b-instruct",
            precision="fp16",
            max_batch_size=8
        )

    def optimize_inference(self, input_text):
        return self.engine.generate(
            input_text,
            max_length=512,
            temperature=0.7
        )
```

### 4. OpenWebUI Integration

```python
from fastapi import FastAPI
from openwebui import WebUI

app = FastAPI()
webui = WebUI(title="Rachel HR Bot")

@app.get("/")
async def root():
    return webui.render(
        template="interview",
        context={
            "mode": "interview",
            "features": ["resume_upload", "real_time_feedback"]
        }
    )
```

## 📝 Usage Guide

1. **Start the Application**
   ```bash
   python run.py
   ```

2. **Access the Interface**
   - Open your browser and navigate to `http://localhost:3000`
   - Log in with your credentials

3. **Upload Resume**
   - Click "Upload Resume" button
   - Select your PDF resume file
   - Wait for analysis completion

4. **Start Interview**
   - Choose your target role
   - Select technical domains
   - Begin interview session

5. **During Interview**
   - Answer questions naturally
   - Receive real-time feedback
   - Use hints when needed
   - Track your progress

## 🤝 Contributing

We welcome contributions! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- NVIDIA for providing advanced AI technologies
- OpenWebUI community for the interface framework
- All contributors and testers

## 📞 Support

- Join our [Discord community](https://discord.gg/rachel-hr-bot)
- Report issues on [GitHub Issues](https://github.com/yourusername/rachel-hr-bot/issues)
- Check out our [Documentation](https://docs.rachel-hr-bot.com)

---

Built with ❤️ by [Your Name] for the NVIDIA and LlamaIndex Developer Contest
