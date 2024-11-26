## Models

## google / gemma-2b

**Model Information**

Gemma is a family of lightweight, state-of-the art open models from Google,built from the same research and technology used to create the Gemini models.They are text-to-text, decoder-only large language models, available in English,with open weights, pre-trained variants, and instruction-tuned variants. Gemma models are well-suited for a variety of text generation tasks, including question answering, summarization, and reasoning. Their relatively small size makes it possible to deploy them in environments with limited resources such as a laptop, desktop or your own cloud infrastructure, democratizing access to \state of the art AI models and helping foster innovation for everyone.

## References:
**Author:** Google

**Model Page:** Gemma

[google / gemma-2b Model](https://docs.api.nvidia.com/nim/reference/google-gemma-2b)
[google / gemma-2b Endpoint](https://docs.api.nvidia.com/nim/reference/google-gemma-2b-infer)
[Model Card](https://ai.google.dev/gemma/docs/model_card)

## Resources and Technical Documentation:

[Responsible Generative AI Toolkit](https://ai.google.dev/responsible)
[Gemma on Kaggle](https://www.kaggle.com/models/google/gemma)
[Gemma on Vertex Model Garden](https://console.cloud.google.com/vertex-ai/publishers/google/model-garden/335?pli=1)

## Third-Party Community Consideration
This model is not owned or developed by NVIDIA. This model has been developed and built to a third-party’s requirements for this application and use case.

**Intended Usage**
Open Large Language Models (LLMs) have a wide range of applications across various industries and domains. The following list of potential uses is not comprehensive. The purpose of this list is to provide contextual information about the possible use-cases that the model creators considered as part of model training and development.

- Content Creation and Communication
  - Text Generation: These models can be used to generate creative text formats such as poems, scripts, code, marketing copy, and email drafts.
  - Chatbots and Conversational AI: Power conversational interfaces for customer service, virtual assistants, or interactive applications.
  - Text Summarization: Generate concise summaries of a text corpus, research papers, or reports.
- Research and Education
  - Natural Language Processing (NLP) Research: These models can serve as a foundation for researchers to experiment with NLPtechniques, develop algorithms, and contribute to the advancement of the field.
  - Language Learning Tools: Support interactive language learning experiences, aiding in grammar correction or providing writing practice.
  - Knowledge Exploration: Assist researchers in exploring large bodies of text by generating summaries or answering questions about specific topics.

## Model Data
**Training Dataset**

These models were trained on a text dataset that includes a wide variety of sources, totaling 6 trillion tokens. Here are the primary training data sources:

- Web Documents: A diverse collection of web text ensures the model is exposed to a broad range of linguistic styles, topics, and vocabulary. Primarily English-language content.
- Code: Exposing the model to code helps it to learn the syntax and patterns of programming languages, which improves its ability to generate code or understand code-related questions.
- Mathematics: Training on mathematical text helps the model learn logical reasoning, symbolic representation, and to address mathematical queries.


The combination of these diverse data sources is crucial for training a powerful language model that can handle a wide variety of different tasks and text formats.

## Data Preprocessing
Here are the key data cleaning and filtering methods applied to the training data:

- CSAM Filtering: Rigorous CSAM (Child Sexual Abuse Material) filtering was applied at multiple stages in the data preparation process to ensure the exclusion of harmful and illegal content.
- Sensitive Data Filtering: As part of making Gemma pre-trained models safe and reliable, automated techniques were used to filter out certain personal information and other sensitive data from training sets.
- Additional methods: Filtering based on content quality and safely in line with our [policies](https://storage.googleapis.com/gweb-uniblog-publish-prod/documents/2023_Google_AI_Principles_Progress_Update.pdf#page=11)


## Implementation Information

**TensorRT-LLM**

The endpoint available on NGC catalog is accelerated by TensorRT-LLM, an open-source library for optimizing inference performance. Gemma is compatible across NVIDIA AI platforms—from the datacenter, cloud, to the local PC with RTX GPU systems.  

Gemma models use a vocabulary size of 256K and support a context length of up to 8K while using rotary positional embedding (RoPE). With support for Position Interpolation (PI) available in TensorRT-LLM, Gemma models using RoPE can support longer output sequence lengths at inference time while retaining original model architecture. 

## Model Customization

The model is converted to .nemo for easy customization with NVIDIA NeMo framework – an end-to-end framework to curate data, tune models, and deploy anywhere. It supports various customization techniques including RLHF, SFT, LoRA, and Steer-LM.

## Evaluation
Model evaluation metrics and results.

## Benefits
At the time of release, this family of models provides high-performance open large language model implementations designed from the ground up for Responsible AI development compared to similarly sized models.

Using the benchmark evaluation metrics described in this document, these models have shown to provide superior performance to other, comparably-sized open model alternatives.


## Request

```
import requests

url = "https://integrate.api.nvidia.com/v1/chat/completions"

payload = {
    "model": "google/gemma-2b",
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
    "authorization": "Bearer nvapi-xxxxx"
}

response = requests.post(url, json=payload, headers=headers)

print(response.text)
```

## Response

```
{
  "id": "chatcmpl-657cab5d-390b-47ed-bfd6-84b4d28c4396",
  "object": "chat.completion",
  "created": 1732296663,
  "model": "google/gemma-2b",
  "choices": [
    {
      "index": 0,
      "message": {
        "role": "assistant",
        "content": "**String** is a fundamental data type in programming that represents a sequence of characters. It is a collection of characters enclosed within double quotes (\").\n\n**Characteristics of a String:**\n\n- Sequence of characters\n- Immutable (cannot be modified after creation)\n- Consists of characters, digits, or a combination of both\n- Can store both simple and complex data\n\n**Operations on Strings:**\n\n- **Length():** Returns the number of characters in a string.\n- **Index():** Returns the position of a character within a string.\n- **Substring():** Extracts a sub-sequence of characters from a string.\n- **Concat():** Combines multiple strings into a single string.\n- **Split():** Divides a string into multiple substrings based on a delimiter.\n\n**Syntax:**\n\n```\nstring = \"Hello World!\"\n```\n\n**Example Usage:**\n\n```python\nmy_string = \"This is a string.\"\n\n# Get the length of the string\nlength = len(my_string)\n\n# Print the first 5 characters of the string\nprint(my_string[:5])\n```\n\n**Benefits of Using Strings:**\n\n- **Data storage:** Efficient way to store and manage large amounts of text data.\n- **Communication:** Allows for the representation of human-readable data.\n- **Algorithm efficiency:** Strings are often used as keys in dictionaries and as input parameters for functions.\n- **Code readability:** Makes code more readable by using meaningful variable names and descriptive string literals.\n\n**Applications of Strings:**\n\n- Web development (HTML, CSS, JavaScript)\n- Data processing and analysis\n- Database management\n- System programming\n- Text manipulation and formatting\n\n**Additional Points:**\n\n- Strings are immutable, meaning their value cannot be changed after creation.\n- Strings can contain special characters and Unicode characters.\n- The type of a string is determined by the programming language or environment in which it is used."
      },
      "logprobs": {
        "text_offset": [],
        "token_logprobs": [
          0,
          0
        ],
        "tokens": [],
        "top_logprobs": []
      }
    }
  ],
  "usage": {
    "prompt_tokens": 14,
    "total_tokens": 420,
    "completion_tokens": 406
  }
}
```


## Shell

## Request

```
curl --request POST \
     --url https://integrate.api.nvidia.com/v1/chat/completions \
     --header 'accept: application/json' \
     --header 'authorization: Bearer xxxxxxxx' \
     --header 'content-type: application/json' \
     --data '
{
  "model": "google/gemma-2b",
  "max_tokens": 1024,
  "stream": false,
  "temperature": 0.5,
  "top_p": 1,
  "stop": null,
  "frequency_penalty": 0,
  "presence_penalty": 0,
  "seed": 0,
  "messages": "string"
}
'
```


## Models

## google / codegemma-7b

CodeGemma is a family of lightweight open code models built on top of Gemma.CodeGemma models are text-to-text and text-to-code decoder-only models and are available as a 7 billion pretrained variant that specializes in code completion and code generation tasks, a 7 billion parameter instruction-tuned variant for code chat and instruction following and a 2 billion parameter pretrained variant
for fast code completion. This model is ready for commercial use.

[google / codegemma-7b Model](https://docs.api.nvidia.com/nim/reference/google-codegemma-7b)
[google / codegemma-7b Endpoint](https://docs.api.nvidia.com/nim/reference/google-codegemma-7b-infer)

## Third-Party Community Consideration
This model is not owned or developed by NVIDIA. This model has been developed and built to a third-party’s requirements for this application and use case; see link to the [CodeGemma Model Card](https://ai.google.dev/gemma/docs/codegemma).

Terms of Use
By accessing this model, you are agreeing to the NVIDIA AI Foundation Models Community License

Additional Information: Gemma Terms of Use, Google Prohibited Use Policy.


## Resources and Technical Documentation
[Responsible Generative AI Toolkit](https://ai.google.dev/responsible)
[CodeGemma on Kaggle](https://www.kaggle.com/models/google/codegemma)


## Model Architecture:
Architecture Type: Transformer Decoder Network

Network Architecture: Real-Gated Linear Recurrent Unit (RG-LRU)


## Implementation Information
Hardware and Frameworks used during training Like
Gemma, CodeGemma was trained on the latest generation of
Tensor Processing Unit (TPU)
hardware (TPUv5e),
using JAX and ML Pathways.


## Evaluation Approach
Code completion benchmarks: HumanEval (HE) Single Line and Multiple Line Infilling
Code generation benchmarks: HumanEval, MBPP, BabelCode (BC)
(C++, C#, Go, Java, JavaScript, Kotlin, Python, Rust)
Q&A: BoolQ, PIQA, TriviaQA
Natural Language: ARC-Challenge, HellaSwag, MMLU, WinoGrande
Math Reasoning: GSM8K, MATH


## Request

```
curl --request POST \
     --url https://integrate.api.nvidia.com/v1/chat/completions \
     --header 'accept: application/json' \
     --header 'authorization: Bearer nvapi-xxxxxx' \
     --header 'content-type: application/json' \
     --data '
{
  "model": "google/codegemma-7b",
  "max_tokens": 1024,
  "stream": false,
  "temperature": 0.5,
  "top_p": 1,
  "stop": null,
  "frequency_penalty": 0,
  "presence_penalty": 0,
  "seed": 0,
  "messages": "string"
}
'
```

## Response

```
{
  "id": "chatcmpl-6e1f3939-667c-46dc-bbd4-89c174aa5855",
  "object": "chat.completion",
  "created": 1732297615,
  "model": "google/codegemma-7b",
  "choices": [
    {
      "index": 0,
      "message": {
        "role": "assistant",
        "content": "**Definition:**\n\nA string is a sequence of characters enclosed in quotes. In Python, strings are immutable, meaning their contents cannot be changed after they are created.\n\n**Creating Strings:**\n\n* Single quotes: `'hello'`\n* Double quotes: `\"hello\"`\n* Triple quotes (for multi-line strings):\n    * `'''hello'''`\n    * `\"\"\"hello\"\"\"`\n\n**String Operations:**\n\n* Concatenation: `+` operator\n* Repetition: `*` operator\n* Slicing: `[]` operator\n* Indexing: accessing individual characters\n* Membership testing: `in` operator\n* String methods (e.g., `len()`, `upper()`, `lower()`, `split()`)\n\n**String Properties:**\n\n* Immutable\n* Ordered sequence of characters\n* Can contain any type of character (letters, numbers, symbols)\n\n**Examples:**\n\n```python\n# Create a string\nmessage = \"Hello, world!\"\n\n# Print the string\nprint(message)\n\n# Concatenate strings\ngreeting = \"Greetings, \" + message\n\n# Repeat a string\nrepeated_message = message * 3\n\n# Slice a string\nfirst_five_chars = message[:5]\n\n# Check if a character is in a string\nif 'w' in message:\n    print(\"The letter 'w' is in the string.\")\n```\n\n**Additional Notes:**\n\n* Strings are case-sensitive.\n* Strings can be indexed and sliced using integer values.\n* There are several built-in functions and methods for working with strings.\n* Python also supports string formatting for creating formatted output."
      },
      "logprobs": {
        "text_offset": [],
        "token_logprobs": [
          0,
          0
        ],
        "tokens": [],
        "top_logprobs": []
      }
    }
  ],
  "usage": {
    "prompt_tokens": 14,
    "total_tokens": 361,
    "completion_tokens": 347
  }
}
```


## Model
[google / gemma-2b](https://docs.api.nvidia.com/nim/reference/google-gemma-2b)

[google / gemma-2-2b-it](https://docs.api.nvidia.com/nim/reference/google-gemma-2-2b-it)

[google / gemma-2-9b-it](https://docs.api.nvidia.com/nim/reference/google-gemma-2-9b-it)

[google / gemma-2-27b-it](https://docs.api.nvidia.com/nim/reference/google-gemma-2-27b-it)

[google / codegemma-7b](https://docs.api.nvidia.com/nim/reference/google-codegemma-7b)

[google / recurrentgemma-2b](https://docs.api.nvidia.com/nim/reference/google-recurrentgemma-2b)

[google / shieldgemma-9b](https://docs.api.nvidia.com/nim/reference/google-shieldgemma-9b)

## Endpoint
[Create chat completion (gemma-2b)](https://docs.api.nvidia.com/nim/reference/google-gemma-2b-infer)

[Create chat completion (gemma-2-2b-it)](https://docs.api.nvidia.com/nim/reference/google-gemma-2-2b-it-infer)

[Create chat completion (gemma-2-9b-it)](https://docs.api.nvidia.com/nim/reference/google-gemma-2-9b-it-infer)

[Create chat completion (gemma-2-27b-it)](https://docs.api.nvidia.com/nim/reference/google-gemma-2-27b-it-infer)

[Create chat completion (codegemma-7b)](https://docs.api.nvidia.com/nim/reference/google-codegemma-7b-infer)

[Create chat completion (recurrentgemma-2b)](https://docs.api.nvidia.com/nim/reference/google-recurrentgemma-2b-infer)

[Create chat completion (shieldgemma-9b)](https://docs.api.nvidia.com/nim/reference/google-shieldgemma-9b-infer)







