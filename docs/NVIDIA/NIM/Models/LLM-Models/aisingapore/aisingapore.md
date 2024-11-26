# Models

## Large Language models**

**LLM APIs:**

**Overview:**

SEA-LION-7B-Instruct is a multilingual model for natural language understanding (NLU), natural language generation (NLG), and natural language reasoning (NLR) tasks that has been fine-tuned with thousands of English and Indonesian instruction-completion pairs alongside a smaller pool of instruction-completion pairs from other Association of Southeast Asian Nations (ASEAN) languages. These instructions have been carefully curated and rewritten to ensure the model was trained on truly open, commercially permissive and high quality datasets. This model is for demonstration purposes and not-for-production usage.

SEA-LION stands for Southeast Asian Languages In One Network.

**Third-Party Community Consideration:** [SEA-LION Model Card](https://huggingface.co/aisingapore/sea-lion-7b-instruct)

**Models**


Endpoint: **Create chat completion (yi-large)**
[Create a chat completion (sea-lion-7b-instruct endpoint](https://docs.api.nvidia.com/nim/reference/create_chat_completion_v1_chat_completions_post)

Model: **Create chat completion (yi-large)**
[aisingapore / sea-lion-7b-instruct model](https://docs.api.nvidia.com/nim/reference/aisingapore-sea-lion-7b-instruct)



Use Cases:


- **Knowledge Search and Query**
- **Data Classification**
- **Chatbots**
- **Customer Service**

**Training Dataset**
SEA-LION-7B-Instruct was trained on a wide range of instructions that were manually and stringently verified by our team. A large portion of the effort was dedicated to ensuring that each instruction-completion pair that the model sees is of a high quality and any errors were corrected and rewritten by native speakers or else dropped from our mix.

In addition, special care was taken to ensure that the datasets used had commercially permissive licenses through verification with the original data source.

**Inference:**
**Engine:** Triton + TensorRT-LLM
**Test Hardware [Name the specific test hardware model]:**
- L40S

## Request

```
import requests

url = "https://integrate.api.nvidia.com/v1/chat/completions"

payload = {
    "model": "aisingapore/sea-lion-7b-instruct",
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
    "authorization": "Bearer xxxxxx"
}

response = requests.post(url, json=payload, headers=headers)

print(response.text)
```


## Response

```
{
  "id": "chatcmpl-c1579c26-979a-4255-b092-9dcda118bdb0",
  "object": "chat.completion",
  "created": 1732276645,
  "model": "aisingapore/sea-lion-7b-instruct",
  "choices": [
    {
      "index": 0,
      "message": {
        "role": "assistant",
        "content": "Laissez les enfants leur faire leurs recettes"
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
          }
        ]
      }
    }
  ],
  "usage": {
    "prompt_tokens": 11,
    "total_tokens": 24,
    "completion_tokens": 13
  }
}
```
