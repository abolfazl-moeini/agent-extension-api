# xAI Developer Portal & API Docs - Get started with xAI

Source: https://docs.x.ai/

---

# Get started with xAI

Build with Grok, the AI model designed to deliver truthful, insightful answers.

## Models

We offer a range of models supporting multiple use cases and modalities.

### [Responses API](/developers/model-capabilities/text/generate-text)

Generate text, have conversations, use tools, and build AI-powered applications.

* Generate text
* Multi-turn chat
* Function calling

### [Voice API](/developers/model-capabilities/audio/text-to-speech)

Convert text to natural speech or transcribe audio with our voice models.

* Text to speech
* Speech to text
* Real-time voice

### [Imagine API (Images)](/developers/model-capabilities/images/generation)

Generate stunning images from text, edit existing images, and understand visual content.

* Generate images
* Edit images
* Precise control

### [Imagine API (Video)](/developers/model-capabilities/video/generation)

Bring an image to life, start from a simple text prompt, or refine a complex cinematic sequence.

* Generate videos
* Edit videos
* Precise control

## Quick Start

```python
from openai import OpenAI

client = OpenAI(
    api_key="YOUR_XAI_API_KEY",
    base_url="https://api.x.ai/v1",
)

response = client.responses.create(
    model="grok-4.3",
    input=[
        {"role": "system", "content": "You are Grok, an AI agent built to answer helpful questions."},
        {"role": "user", "content": "How big is the universe?"},
    ],
)

print(response.output_text)
```

```bash
curl https://api.x.ai/v1/responses \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $XAI_API_KEY" \
  -d '{
    "model": "grok-4.3",
    "input": [
        {
            "role": "system",
            "content": "You are Grok, an AI agent built to answer helpful questions."
        },
        {
            "role": "user",
            "content": "How big is the universe?"
        }
    ]
}'
```

## Get Started

* [Quickstart guide](/developers/quickstart)
* [Models](/developers/models)
* [Pricing](/developers/pricing)

## Build

* [Function calling](/developers/tools/function-calling)
* [Web search](/developers/tools/web-search)
* [Structured outputs](/developers/model-capabilities/text/structured-outputs)
* [Batch API](/developers/advanced-api-usage/batch-api)

## Resources

* [API reference](/developers/rest-api-reference/inference)
* [Cookbook](/cookbook)
* [Community integrations](/developers/community)
* [Release notes](/developers/release-notes)