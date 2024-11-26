# Models

## databricks / dbrx-instruct


**Model Information**
DBRX is a transformer-based decoder-only large language model (LLM) that was trained using next-token prediction. It uses a fine-grained mixture-of-experts (MoE) architecture with 132B total parameters of which 36B parameters are active on any input.

Compared to other open MoE models like Mixtral-8x7B and Grok-1, DBRX is fine-grained, meaning it uses a larger number of smaller experts. DBRX has 16 experts and chooses 4, while Mixtral-8x7B and Grok-1 have 8 experts and choose 2. This provides 65x more possible combinations of experts and we found that this improves model quality. DBRX uses rotary position encodings (RoPE), gated linear units (GLU), and grouped query attention (GQA). It uses a converted version of the GPT-4 tokenizer as defined in the tiktoken repository. We made these choices based on exhaustive evaluation and scaling experiments.

[databricks / dbrx-instruct Model](https://docs.api.nvidia.com/nim/reference/databricks-dbrx-instruct)
[databricks / dbrx-instruct Endpoint](https://docs.api.nvidia.com/nim/reference/databricks-dbrx-instruct-infer)
## Third-Party Community Consideration

This model is not owned or developed by NVIDIA. This model has been developed and built to a third-party’s requirements for this application and use case; see link to Non-NVIDIA

[DBRX Model Card](https://huggingface.co/databricks/dbrx-instruct)

## License and Terms of use
GOVERNING TERMS: Your use of this API is governed by the NVIDIA API Trial Service Terms of Use; and the use of this model is governed by the NVIDIA AI Foundation Models Community License and Databricks Open Model License.

## Model Architecture:
**Architecture Type**: Transformer

## Training, Testing, and Evaluation Datasets:
**Training Dataset:**
Properties (Quantity, Dataset Descriptions, Sensor(s)): Pre-trained on 12T tokens of text and code data.

**Inference:**
**Engine:** Triton, TRT-LLM

**Test Hardware:** H100


## Request

```
import requests

url = "https://integrate.api.nvidia.com/v1/chat/completions"

payload = {
    "model": "databricks/dbrx-instruct",
    "max_tokens": 1024,
    "stream": False,
    "temperature": 0.5,
    "top_p": 1,
    "stop": None,
    "frequency_penalty": 0,
    "presence_penalty": 0,
    "seed": 0,
    "messages": "string"
}
headers = {
    "accept": "application/json",
    "content-type": "application/json",
    "authorization": "Bearer nvapi-xxxxxx"
}

response = requests.post(url, json=payload, headers=headers)

print(response.text)
```

## Response

```
{
  "id": "chatcmpl-b7a187d9-5921-4eac-87fb-e8d2d732e7a9",
  "object": "chat.completion",
  "created": 1732294663,
  "model": "databricks/dbrx-instruct",
  "choices": [
    {
      "index": 0,
      "message": {
        "role": "assistant",
        "content": "Hello! I'm here to help you with any questions or tasks you have, to the best of my ability. Let's get started! How can I assist you today?"
      },
      "logprobs": {
        "content": [
          {
            "logprob": 0
          },
          {
            "logprob": 0
          },
          {
            "logprob": 0
          },
          {
            "logprob": 0
          },
          {
            "logprob": 0
          },
          {
            "logprob": 0
          },
          {
            "logprob": 0
          },
          {
            "logprob": 0
          },
          {
            "logprob": 0
          },
          {
            "logprob": 0
          },
          {
            "logprob": 0
          },
          {
            "logprob": 0
          },
          {
            "logprob": 0
          },
          {
            "logprob": 0
          },
          {
            "logprob": 0
          },
          {
            "logprob": 0
          },
          {
            "logprob": 0
          },
          {
            "logprob": 0
          },
          {
            "logprob": 0
          },
          {
            "logprob": 0
          },
          {
            "logprob": 0
          },
          {
            "logprob": 0
          },
          {
            "logprob": 0
          },
          {
            "logprob": 0
          },
          {
            "logprob": 0
          },
          {
            "logprob": 0
          },
          {
            "logprob": 0
          },
          {
            "logprob": 0
          },
          {
            "logprob": 0
          },
          {
            "logprob": 0
          },
          {
            "logprob": 0
          },
          {
            "logprob": 0
          },
          {
            "logprob": 0
          },
          {
            "logprob": 0
          },
          {
            "logprob": 0
          }
        ]
      }
    }
  ],
  "usage": {
    "prompt_tokens": 225,
    "total_tokens": 260,
    "completion_tokens": 35
  }
}
```
