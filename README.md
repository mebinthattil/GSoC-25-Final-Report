## Final Report

### Links to Proof Of Work:
- [PR Speak-AI](https://github.com/sugarlabs/speak-ai/pull/1)
- Deployment of [ai.sugarlabs.org](https://ai.sugarlabs.org/)
- [16+ fine-tuned models](https://huggingface.co/MebinThattil/models) on Hugging Face
- [CI/CD for Sugar-AI](https://github.com/sugarlabs/sugar-ai/pull/32)
---
- [Educational Dataset](https://github.com/mebinthattil/Education-Dialogue-Dataset)
- [Voice Testing](https://newstreamlit-frontend.blackpond-9921706d.eastus.azurecontainerapps.io/)
- [Model Benchmarking](https://llm-benchmarking-sugar.streamlit.app/)
- [SLM Comparison](https://slm-benchmark.streamlit.app/)

### **Project Overview**

The objective of this GSoC project was to **modernize and enhance the Speak Activity** using gen-AI and transforming it from a simple text-to-speech tool into an intelligent, conversational learning companion. The project aimed to integrate modern TTS models, deploy both local Small Language Models (SLMs) and cloud-hosted Large Language Models (LLMs), and create an engaging persona-based interaction system for children.

### **Key Deliverables**
1. **Modern TTS Integration** - Replaced traditional espeak with Kokoro TTS for natural-sounding, multi-voice audio generation
2. **Dual Model System For Chatbot Brains** - Implemented both local SLM and cloud LLM as part of the chatbot mode
3. **SugarAI** - Deployed cloud infrastructure at [ai.sugarlabs.org](https://ai.sugarlabs.org) for hosting the LLMs. Used by other activities as well.
4. **Interactive Personas** - Created character based learning experiences with unique voices and personalities
5. **Comprehensive Safety Features** - Built profanity filters and child safe interaction mechanisms

All features are optimized for educational environments and resource constrained devices.

---

### **Project Timeline and Achievements**

#### **Phase 1: Research and Benchmarking (Weeks 1-3)**

**Week 1: Model Selection and Benchmarking**
- **LLM/SLM Evaluation:** Created a [Streamlit benchmarking app](https://llm-benchmarking-sugar.streamlit.app/) to compare different models
- **Dual-Model Architecture Discovery:** Experimented with generation + refinement approach using Gemma3-1B, achieving performance comparable to 30B parameter models
- **Resource Constraint Analysis:** Identified need for models under 100MB for packaging with Speak activity

**Week 2: Fine-tuning Infrastructure and Dataset Development**
- **AWS SageMaker Setup:** Provisioned GPU infrastructure for model training on `ml.g5.2xlarge` instances
- **Educational Dataset Creation:** Developed and cleaned [Education-Dialogue-Dataset](https://github.com/mebinthattil/Education-Dialogue-Dataset) with teacher-student conversations
- **Model Training:** Fine-tuned Llama3-1B with educational conversation patterns
- **Deployment Infrastructure:** Created model storage and API endpoint systems on AWS

**Week 3: Dataset Restructuring and Optimization**
- **Conversation Format Refinement:** Restructured dataset to prevent chain response generation issues
- **Model Behavior Analysis:** Identified and resolved conversational flow problems in fine tuned models
- **Training Optimization:** Developed improved training approaches for educational use cases

---

#### **Phase 2: TTS Integration and Voice Development (Weeks 4-6)**

**Week 4: Kokoro TTS Integration**
- **Modern TTS Implementation:** Successfully integrated Kokoro TTS with minimal additional dependencies
- **Voice Catalog Access:** Enabled entire collection of Kokoro voices for different personas
- **Audio Pipeline Development:** Built temporary WAV file approach as initial implementation
- **Dependency Optimization:** Swapped Kokoro's fallback from espeak-ng to espeak to reduce dependencies
- **Community Testing Platform:** Deployed [voice mixing web app](https://newstreamlit-frontend.blackpond-9921706d.eastus.azurecontainerapps.io/) for feedback collection

**Week 5: SLM Development and Quantization**
- **Lightweight Model Training:** Fine-tuned [Llama 135M](https://huggingface.co/amd/AMD-Llama-135m) on educational dataset
- **Size Optimization:** Achieved ~500MB model size with potential for further quantization
- **Performance Evaluation:** Benchmarked model performance against larger alternatives
- **Dataset Quality Improvement:** Enhanced training data with better conversational patterns

**Week 6: Dataset Enhancement and Performance Optimization**
- **Comprehensive Dataset Revision:** Created higher-quality training data using Gemini for teacher-child conversation patterns
- **Model Re-training:** Conducted multiple fine-tuning iterations with improved datasets
- **Performance Analysis:** Formal benchmarking against 50-question evaluation set
- **Size Constraint Solutions:** Achieved critical component sizes:
  - **TTS:** 0.7MB base + 0.5MB per additional voice
  - **SLM:** 82.6MB
  - **Llama.cpp:** 2MB (if using distributed binaries)

---

#### **Phase 3: Infrastructure and Streaming Optimization (Weeks 7-9)**

**Week 7: Community Feedback and Platform Deployment**
- **Comprehensive Model Benchmarking:** Added all 16 fine-tuned SLM variants to [benchmark comparison](https://slm-benchmark.streamlit.app/)
- **AWS Infrastructure Success:** Secured G-series GPU instances after multiple service limit requests
- **Model Repository Organization:** Created [comprehensive model collection](https://huggingface.co/MebinThattil/models) on Hugging Face
- **Community Evaluation Platform:** Deployed benchmarking tools for community model selection

**Week 8: Audio Streaming and Safety Features**
- **GStreamer Optimization:** Implemented direct audio streaming from Kokoro to GStreamer using `appsrc` element
- **Platform-Agnostic Inference:** Replaced compiled binaries with `llama-cpp-python` for cross-platform compatibility
- **Safety Implementation:** Built comprehensive profanity filtering system with base64-encoded word lists
- **Latency Reduction:** Achieved significant performance improvements through streaming architecture

**Week 9: Critical Bug Fixes and System Integration**
- **Mouth Movement Synchronization:** Resolved timing issues through three iterations of optimization
- **Audio Pipeline Sync:** Achieved synchronization between voice output and mouth movements
- **System Architecture Completion:** Integrated all components into cohesive Speak activity

---

#### **Phase 4: Cloud Infrastructure and Final Integration (Weeks 10-12)**

**Week 10: SugarAI Deployment**
- **Cloud Infrastructure:** Successfully deployed SugarAI on AWS EC2 with G5 GPUs
- **Containers:** Implemented Docker-based deployment with GPU acceleration
- **Network Security:** Configured secure inbound rules limiting access to HTTPS and SSH only
- **Service Architecture:** Established foundation for public API accessibility

**Week 11: Production Deployment and Security**
- **SSL Certificate Integration:** Implemented Let's Encrypt certificates for secure HTTPS access
- **Nginx Proxy Configuration:** Created proxy setup mapping internal services to public endpoints
- **DNS Configuration:** Established A record for [ai.sugarlabs.org](https://ai.sugarlabs.org) domain
- **Authentication Systems:** Integrated Google OAuth under Sugar Labs organization
- **Public API Launch:** Made SugarAI publicly accessible with comprehensive API documentation

**Week 12: Complete System Integration**
- **LLM Integration:** Connected cloud-hosted LLM to Speak activity for enhanced conversations
- **Intelligent Mode Switching:** Implemented automatic fallback between LLM (online) and SLM (offline) based on connectivity
- **Personas System:** Deployed character-based learning with unique voices and personalities
- **UI Enhancement:** Complete interface update accommodating all new AI-powered features
- **Production Demo:** Created comprehensive demonstration showcasing all integrated features

---

### **Repositories and Resources**

#### **Core Repositories**
- [SpeakAI Activity](https://github.com/sugarlabs/speak-ai)
- [PR to SpeakAI](https://github.com/sugarlabs/speak-ai/pull/1)
- [Benchmarking Tools](https://github.com/mebinthattil/LLM-benchmarking)
- [Educational Dataset](https://github.com/mebinthattil/Education-Dialogue-Dataset)
- [Model Archive](https://github.com/mebinthattil/Fine-Tune-Attempts-LlaMA-135)
- [Kokoro Integration](https://github.com/mebinthattil/Kokoro-FastAPI)

#### **Testing Platforms**
- [Model Benchmarking](https://llm-benchmarking-sugar.streamlit.app/)
- [SLM Comparison](https://slm-benchmark.streamlit.app/)
- [Voice Testing](https://newstreamlit-frontend.blackpond-9921706d.eastus.azurecontainerapps.io/)

#### **Model Collection**
[16+ fine-tuned models](https://huggingface.co/MebinThattil/models) on Hugging Face

---

### **Acknowledgments**

Thanks to mentors **Chihurumnaya Ibiam** and **Kshitij Shah**, assisting mentors **Walter Bender** and **Devin Ulibarri**, and the Sugar Labs community.

---

### **Conclusion**

This project transformed the Speak Activity from basic text-to-speech into an intelligent learning companion. The hybrid model architecture ensures accessibility regardless of connectivity, while personas make learning engaging through specialized characters. The SugarAI platform provides scalable infrastructure for future Sugar activities.

The modernized Speak activity demonstrates how AI can enhance education while maintaining offline functionality and resource efficiency for all students globally.

---