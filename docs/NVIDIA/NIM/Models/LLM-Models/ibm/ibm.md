## Models

## ibm / granite-34b-code-instruct

## Model Overview
Granite-34B-Code-Instruct generates, explains, and translates code from a natural language prompt. It is a 34B parameter model fine tuned from Granite-34B-Code-Base on a combination of permissively licensed instruction data to enhance instruction following capabilities including logical reasoning and problem-solving skills. This model is ready for commercial use.


[ibm / granite-34b-code-instruct Model](https://docs.api.nvidia.com/nim/reference/ibm-granite-34b-code-instruct)
[ibm / granite-34b-code-instruct Endpoint](https://docs.api.nvidia.com/nim/reference/ibm-granite-34b-code-instruct-infer)

## Third-Party Community Consideration
This model is not owned or developed by NVIDIA. This model has been developed and built to a third-party’s requirements for this application and use case; see link to the [Granite-34B-Code-Instruct Model Card](https://huggingface.co/ibm-granite/granite-34b-code-instruct-8k)

## License and Terms of use
GOVERNING TERMS: Your use of this API is governed by the NVIDIA API Trial Service Terms of Use; and the use of this model is governed by the NVIDIA AI Foundation Models Community License and Apache 2.0 License.

Model Developer: IBM Research

## Model Architecture

Architecture Type: Transformer
Network Architecture: GPT Big Code

## Software Integration:
Supported Hardware Platform(s): NVIDIA Hopper

## Training Data
Granite Code Instruct models are trained on the following types of data.

- Code Commits Datasets: we sourced code commits data from the [CommitPackFT dataset](https://huggingface.co/datasets/bigcode/commitpackft), a filtered version of the full CommitPack dataset. From CommitPackFT dataset, we only consider data for 92 programming languages. Our inclusion criteria boils down to selecting programming languages common across CommitPackFT and the 116 languages that we considered to pretrain the code-base model (Granite-8B-Code-Base).
- Math Datasets: We consider two high-quality math datasets, [MathInstruct](https://huggingface.co/datasets/TIGER-Lab/MathInstruct) and [MetaMathQA](https://huggingface.co/datasets/meta-math/MetaMathQA). Due to license issues, we filtered out GSM8K-RFT and Camel-Math from MathInstruct dataset.
- Code Instruction Datasets: We use [Glaive-Code-Assistant-v3](https://huggingface.co/datasets/glaiveai/glaive-code-assistant-v3), [Glaive-Function-Calling-v2](https://huggingface.co/datasets/glaiveai/glaive-function-calling-v2), [NL2SQL11](https://huggingface.co/datasets/bugdaryan/sql-create-context-instruction) and a small collection of synthetic API calling datasets.
- Language Instruction Datasets: We include high-quality datasets such as [HelpSteer](https://huggingface.co/datasets/nvidia/HelpSteer) and an open license-filtered version of [Platypus](https://huggingface.co/datasets/garage-bAInd/Open-Platypus). We also include a collection of hardcoded prompts to ensure our model generates correct outputs given inquiries about its name or developers.


## Inference
Engine: Triton + TensorRT-LLM

Test Hardware: H100


## Request

```
curl --request POST \
     --url https://integrate.api.nvidia.com/v1/chat/completions \
     --header 'accept: application/json' \
     --header 'authorization: Bearer nvapi-xxxxxxxx' \
     --header 'content-type: application/json' \
     --data '
{
  "model": "ibm/granite-34b-code-instruct",
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
  "id": "chatcmpl-9613fc23-e3d5-412b-8f7f-257296689241",
  "object": "chat.completion",
  "created": 1732299522,
  "model": "ibm/granite-34b-code-instruct",
  "choices": [
    {
      "index": 0,
      "message": {
        "role": "assistant",
        "content": "String is a data type in Python that represents a sequence of characters. It is one of the most commonly used data types in programming, and it is used to store and manipulate textual data. Strings can be created using either single quotes or double quotes, and they can contain any combination of characters, including numbers, letters, whitespace, and special characters.\n\nIn Python, strings can be concatenated using the \"+\" operator, and they can be repeated using the \"*\" operator. Strings can also be indexed and sliced to access specific parts of the string. String methods, such as len() and upper(), can be used to perform various operations on strings.\n\nStrings are an important data type in Python because they allow programmers to store and manipulate textual data in their programs. They can be used to create user interfaces, process text files, and perform various other tasks that require the manipulation of text."
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
    "prompt_tokens": 9,
    "total_tokens": 193,
    "completion_tokens": 184
  }
}
```