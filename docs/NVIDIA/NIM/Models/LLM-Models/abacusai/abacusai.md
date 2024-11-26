# Models

## Large Language models**

**LLM APIs:**

## abacusai / dracarys-llama-3.1-70b-instruct
**Dracarys-Llama-3.1-70B-Instruct**

Endpoint: **Create chat completion (yi-large)**
[abacusai / dracarys-llama-3.1-70b-instruct endpoint](https://docs.api.nvidia.com/nim/reference/abacusai-dracarys-llama-3_1-70b-instruct)

Model: **Create chat completion (yi-large)**
[abacusai / dracarys-llama-3.1-70b-instruct model](https://docs.api.nvidia.com/nim/reference/abacusai-dracarys-llama-3_1-70b-instruct-infer)

Model Details:

- **Developed by:** Abacus.AI
- **Finetuned from model:** [Finetuned from model](https://huggingface.co/meta-llama/Llama-3.1-70B-Instruct)


**Model Architecture**

**Architecture Type:** Transformer

**Inference**
**Engine:** TensorRT-LLM

**Test Hardware:**
- NVIDIA H100x2


## Request

```
import requests

url = "https://integrate.api.nvidia.com/v1/chat/completions"

payload = {
    "model": "abacusai/dracarys-llama-3.1-70b-instruct",
    "max_tokens": 1024,
    "stream": False,
    "temperature": 0.5,
    "top_p": 1,
    "stop": None,
    "frequency_penalty": 0,
    "presence_penalty": 0,
    "messages": [
        {
            "role": "user",
            "content": "Write code to select rows from the dataframe `df` having the maximum `temp` for each `city`."
        }
    ]
}
headers = {
    "accept": "application/json",
    "content-type": "application/json",
    "authorization": "Bearer  xxxxxxxx"
}

response = requests.post(url, json=payload, headers=headers)

print(response.text)
```

## Response

```
{
  "id": "chat-298ca81391884a689066eb7ed9f54795",
  "object": "chat.completion",
  "created": 1732275965,
  "model": "abacusai/dracarys-llama-3.1-70b-instruct",
  "choices": [
    {
      "index": 0,
      "message": {
        "role": "assistant",
        "content": "Here is a Python code snippet using pandas that selects rows from a DataFrame `df` having the maximum `temp` for each `city`:\n\n```python\nimport pandas as pd\n\n# Assuming df is your DataFrame with columns 'city' and 'temp'\n\n# Group by 'city' and get the index of the row with the maximum 'temp' for each city\nmax_temp_indices = df.groupby('city')['temp'].idxmax()\n\n# Select rows from df using the indices obtained above\nmax_temp_rows = df.loc[max_temp_indices]\n\nprint(max_temp_rows)\n```\n\n### Explanation:\n\n1. **Grouping**: The `groupby` function is used to group the DataFrame `df` by the `city` column. This allows us to perform operations on each group of rows that share the same `city` value.\n\n2. **Finding Maximum Temperature**: The `idxmax` function is applied to the `temp` column within each group. This returns the index of the row with the maximum `temp` value for each `city`.\n\n3. **Selecting Rows**: The `loc` function is used to select rows from `df` based on the indices obtained from `idxmax`. This gives us a new DataFrame `max_temp_rows` containing only the rows where the `temp` is maximum for each `city`.\n\n### Example Use Case:\n\nSuppose you have a DataFrame `df` like this:\n\n```markdown\n| city   | temp |\n|--------|------|\n| NewYork| 25   |\n| NewYork| 30   |\n| London | 18   |\n| London | 20   |\n| Paris  | 22   |\n| Paris  | 25   |\n```\n\nRunning the code will output:\n\n```markdown\n| city   | temp |\n|--------|------|\n| NewYork| 30   |\n| London | 20   |\n| Paris  | 25   |\n```\n\nThis output shows the rows with the maximum `temp` for each `city`."
      },
      "logprobs": null,
      "finish_reason": "stop",
      "stop_reason": null
    }
  ],
  "usage": {
    "prompt_tokens": 32,
    "total_tokens": 442,
    "completion_tokens": 410
  },
  "prompt_logprobs": null
}
```