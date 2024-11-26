## Models

## deepseek-ai / deepseek-coder-6.7b-instruct

**Model Overview**
DeepSeek Coder is a series of code language models trained from scratch on 2T tokens, comprising 87% code and 13% natural language in English and Chinese. These models are available in sizes ranging from 1B to 33B parameters and are designed to support project-level code completion and infilling. The 6.7B parameter model, deepSeek-coder-6.7b-instruct, is fine-tuned on 2B tokens of instruction data and offers state-of-the-art performance on multiple programming languages and benchmarks.

[deepseek-ai / deepseek-coder-6.7b-instruct Model](https://docs.api.nvidia.com/nim/reference/deepseek-ai-deepseek-coder-6_7b-instruct)
[deepseek-ai / deepseek-coder-6.7b-instruct Endpoint](https://docs.api.nvidia.com/nim/reference/deepseek-ai-deepseek-coder-6_7b-instruct-infer)


## Third-Party Community Consideration

This model is not owned or developed by NVIDIA. This model has been developed and built to a third-party’s requirements for this application and use case; see link to the [deepseek-coder-6.7b-instruct](https://huggingface.co/deepseek-ai/deepseek-coder-6.7b-instruct) on Hugging Face.


**Terms of Use**
GOVERNING TERMS: The use of this model is subject to the MIT License and DeepSeek AI Model Agreement.

## Model Architecture:
**Architecture Type:** Generative Pre-Trained Transformer (GPT)-based

**Network Architecture:** Pre-trained on project-level code corpus with a window size of 16K and a fill-in-the-blank task

**Supported Hardware Platform(s):** NVIDIA L4 GPUs

## Inference:
**Engine:** Triton


## Request

```
import requests

url = "https://integrate.api.nvidia.com/v1/chat/completions"

payload = {
    "model": "deepseek-ai/deepseek-coder-6.7b-instruct",
    "max_tokens": 1024,
    "stream": False,
    "temperature": 0.5,
    "top_p": 1,
    "frequency_penalty": 0,
    "presence_penalty": 0,
    "seed": 0,
    "messages": [
        {
            "content": "write a quick sort algorithm in python.",
            "role": "user"
        }
    ]
}
headers = {
    "accept": "application/json",
    "content-type": "application/json",
    "authorization": "Bearer nvapi-xxxx"
}

response = requests.post(url, json=payload, headers=headers)

print(response.text)
```

## Response

```
{
  "id": "cmpl-0d141da83958495ab0cf4b69de49e050",
  "object": "chat.completion",
  "created": 1732295074,
  "model": "deepseek-ai/deepseek-coder-6.7b-instruct",
  "choices": [
    {
      "index": 0,
      "message": {
        "role": "assistant",
        "content": "Sure, here is a simple implementation of the Quick Sort algorithm in Python:\n\n```python\ndef quick_sort(arr):\n    if len(arr) <= 1:\n        return arr\n    else:\n        pivot = arr[0]\n        less_than_pivot = [x for x in arr[1:] if x <= pivot]\n        greater_than_pivot = [x for x in arr[1:] if x > pivot]\n        return quick_sort(less_than_pivot) + [pivot] + quick_sort(greater_than_pivot)\n\n# Test the function\narr = [10, 7, 8, 9, 1, 5]\nprint(quick_sort(arr))\n```\n\nThis algorithm works by selecting a 'pivot' element from the array and partitioning the other elements into two sub-arrays, according to whether they are less than or greater than the pivot. The sub-arrays are then recursively sorted.\n"
      },
      "logprobs": null,
      "finish_reason": "stop",
      "stop_reason": null
    }
  ],
  "usage": {
    "prompt_tokens": 77,
    "total_tokens": 306,
    "completion_tokens": 229
  }
}
```
