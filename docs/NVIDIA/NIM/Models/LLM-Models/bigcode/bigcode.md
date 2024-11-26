# Models

1. **bigcode / starcoder2-7b**

**StarCoder2 Model Overview**
StarCoder2-7b is a state-of-the-art language model with 7 billion parameters, trained on 17 programming languages using The Stack v2 dataset. It employs advanced techniques like Grouped Query Attention and sliding window attention to enhance its performance on coding tasks. The model is optimized to handle a context window of 16,384 tokens and was trained using the Fill-in-the-Middle objective on 3.5+ trillion tokens.

[ StarCoder2-7b on Hugging Face ](https://huggingface.co/bigcode/starcoder2-7b)
[ StarCoder2-7b endpoint ](https://docs.api.nvidia.com/nim/reference/bigcode-starcoder2-7b-infer)

**Model Architecture:**

**Architecture Type:** Transformer decoder

**Supported Hardware Platform(s):** NVIDIA L4 GPUs

## Inference:**
**Engine:** Triton Inference Server
**Test Hardware:** NVIDIA L4 systems

## Request

```
import requests

url = "https://integrate.api.nvidia.com/v1/completions"

payload = {
    "model": "bigcode/starcoder2-7b",
    "prompt": "# Python function that finds primes:",
    "max_tokens": 200,
    "temperature": 0.1,
    "top_p": 1,
    "frequency_penalty": 0,
    "presence_penalty": 0,
    "seed": 0
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
  "id": "cmpl-5d67317a-9dc8-4149-a794-ec85249c2647",
  "object": "text_completion",
  "created": 1732293949,
  "model": "bigcode/starcoder2-7b",
  "choices": [
    {
      "index": 0,
      "text": "\ndef is_prime(n):\n    if n == 2:\n        return True\n    if n % 2 == 0 or n <= 1:\n        return False\n    sqr = int(math.sqrt(n)) + 1\n    for divisor in range(3, sqr, 2):\n        if n % divisor == 0:\n            return False\n    return True\n\n# Python function that finds the largest prime factor of a number:\ndef largest_prime_factor(n):\n    largest_prime = 1\n    for i in range(2, n):\n        if n % i == 0 and is_prime(i):\n            largest_prime = i\n    return largest_prime\n\n# Python function that finds the sum of the digits of a number:\ndef sum_digits(n):\n    sum = 0\n    while n > 0:\n        sum += n % 10\n        n //= 10\n   ",
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
          }
        ]
      }
    }
  ],
  "usage": {
    "prompt_tokens": 8,
    "total_tokens": 208,
    "completion_tokens": 200
  }
}
```

