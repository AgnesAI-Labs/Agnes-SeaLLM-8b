# Agnes-SeaLLM-8B

<p align="center">
  <a href="https://huggingface.co/Agnes-AI/Agnes-SeaLLM-8b"><img src="https://img.shields.io/badge/Hugging%20Face-Agnes--SeaLLM--8B-FFD21E?style=for-the-badge" alt="Hugging Face"></a>
  <a href="https://github.com/AgnesAI-Labs"><img src="https://img.shields.io/badge/GitHub-AgnesAI--Labs-24292F?style=for-the-badge" alt="AgnesAI-Labs"></a>
  <a href="https://huggingface.co/Agnes-AI/Agnes-SeaLLM-8b"><img src="https://img.shields.io/badge/License-Apache--2.0-0A66C2?style=for-the-badge" alt="Apache-2.0"></a>
</p>

Official GitHub landing page for **Agnes-SeaLLM-8B**, an open-source multilingual 8B language model optimized for Southeast Asian language use cases.

The model weights are hosted on Hugging Face:

- Model repository: https://huggingface.co/Agnes-AI/Agnes-SeaLLM-8b
- License: Apache-2.0
- Primary format: Safetensors
- Task: Text generation
- Last updated: 2026-06-24

## Overview

Agnes-SeaLLM-8B is designed for multilingual reasoning, translation, instruction following, and conversational applications across Southeast Asian language contexts.

This GitHub repository is the official coordination and documentation entry point. It does **not** mirror the full model weights because the Hugging Face repository is the canonical model hosting location and the model files are large.

## Model Highlights

- 8B-class compact deployment footprint
- Southeast Asian multilingual optimization
- Instruction-following and dialogue-oriented usage
- Safetensors model format
- Compatible with Transformers, vLLM, SGLang, and Docker-based local serving workflows

## Quick Start

### Transformers

```python
from transformers import AutoTokenizer, AutoModelForCausalLM

model_id = "Agnes-AI/Agnes-SeaLLM-8b"

tokenizer = AutoTokenizer.from_pretrained(model_id)
model = AutoModelForCausalLM.from_pretrained(model_id)

messages = [
    {"role": "user", "content": "Who are you?"}
]

inputs = tokenizer.apply_chat_template(
    messages,
    add_generation_prompt=True,
    tokenize=True,
    return_dict=True,
    return_tensors="pt",
).to(model.device)

outputs = model.generate(**inputs, max_new_tokens=128)
print(tokenizer.decode(outputs[0][inputs["input_ids"].shape[-1]:]))
```

### vLLM

```bash
pip install vllm
vllm serve "Agnes-AI/Agnes-SeaLLM-8b"
```

```bash
curl -X POST "http://localhost:8000/v1/chat/completions" \
  -H "Content-Type: application/json" \
  --data '{
    "model": "Agnes-AI/Agnes-SeaLLM-8b",
    "messages": [
      {
        "role": "user",
        "content": "What is the capital of France?"
      }
    ]
  }'
```

### SGLang

```bash
pip install sglang
python3 -m sglang.launch_server \
  --model-path "Agnes-AI/Agnes-SeaLLM-8b" \
  --host 0.0.0.0 \
  --port 30000
```

## Repository Scope

This GitHub repository is intended for:

- Official model announcements and documentation
- Usage examples and integration notes
- Issue tracking for documentation, reproducibility, and integration questions
- Links to Hugging Face-hosted weights and model assets

Large model files remain on Hugging Face.

## Links

- Hugging Face model: https://huggingface.co/Agnes-AI/Agnes-SeaLLM-8b
- Agnes AI GitHub organization: https://github.com/AgnesAI-Labs
- Agnes AI website: https://agnes-ai.com/

## License

Agnes-SeaLLM-8B is released under the Apache-2.0 license. See the Hugging Face model page for the source model card and license metadata.
