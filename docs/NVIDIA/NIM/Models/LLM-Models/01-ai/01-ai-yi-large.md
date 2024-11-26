# Models

## Large Language models

**LLM APIs:**

Overview:
The Large Language Model (LLM) NIM API endpoints provide simple access to use natural language based generative AI.
This single API endpoint provides access to top models for use in a wide range of tasks including: chat, instruction following, question answering, summarization, creative text generation, and code generation.

NOTE: Select models are available as downloadable container images and supported with an NVIDIA AI Enterprise entitlement.These select models have additional OpenAI API spec details for running self-hosted localized NIMs.

**Models**

1. **01-ai**

Endpoint: **Create chat completion (yi-large)**
[yi-large endpoint](https://docs.api.nvidia.com/nim/reference/01-ai-yi-large)

Model: **Create chat completion (yi-large)**
[yi-large model](https://docs.api.nvidia.com/nim/reference/01-ai-yi-large-infer)


Yi-Large is a model for generating code as well as logic and mathematical reasoning. It is the latest proprietary dense model of the Yi Series State of the Art Large Language Models from 01.AI. The model was trained with significant improvement from

Use Cases:
Seamlessly integrating with the OpenAI API, the Yi Model API offers
compatibility with minimal code adjustments for a smooth transition.

- **Knowledge Search and Query**
- **Data Classification**
- **Chatbots**
- **Customer Service**

Training Dataset
Yi-Large has been trained from scratch using a multilingual tokenizer
and multilingual data in pre-training including English, Chinese,
Spanish, and Japanese, to name a few. Data quality was rigorously
ensured throughout.

**Inference:**
**Engine:** Tensor(RT)-LLM
**Test Hardware [Name the specific test hardware model]:**
- NVIDIA A800 (80G)


```
curl --request POST \
     --url https://httpbin.org/anything/bearer
     --header 'Authorization: Bearer  xxxxxxxxxxx'
```

```
python -m pip install requests
```

## Request

```
import requests

url = "https://integrate.api.nvidia.com/v1/chat/completions"

payload = {
    "model": "01-ai/yi-large",
    "messages": [
        {
            "content": "I am going to Paris, what should I see?",
            "role": "user"
        }
    ],
    "temperature": 0.2,
    "top_p": 0.7,
    "frequency_penalty": 0,
    "presence_penalty": 0,
    "max_tokens": 1024,
    "stream": False,
    "stop": ["string"]
}
headers = {
    "accept": "application/json",
    "content-type": "application/json",
    "authorization": "Bearer  xxxxxxxxxx"
}

response = requests.post(url, json=payload, headers=headers)

print(response.text)
```

## Response

```
{
  "id": "cmpl-7ca0d306a1524ac1a1c403fc235b86cc",
  "object": "chat.completion",
  "created": 1732263955,
  "model": "01-ai/yi-large",
  "choices": [
    {
      "index": 0,
      "message": {
        "role": "assistant",
        "content": "Paris, the capital city of France, is renowned for its art, fashion, gastronomy, and culture, making it a must-visit destination for travelers from around the globe. Here's a list of some of the top attractions and experiences you shouldn't miss during your visit to Paris:\n\n1. **Eiffel Tower**: An iconic symbol of Paris, climbing to the top of the Eiffel Tower offers breathtaking views of the city. It's best to buy tickets in advance to avoid long queues.\n\n2. **Louvre Museum**: Home to thousands of works of art, including the Mona Lisa and the Venus de Milo, the Louvre is the world's largest art museum and a historic monument in Paris.\n\n3. **Notre-Dame Cathedral**: Although it suffered a significant fire in 2019, Notre-Dame remains a symbol of French Christianity and French architecture. Check for updates on its current status and possible visits.\n\n4. **Montmartre and Sacré-Cœur**: The Sacré-Cœur Basilica, located in the Montmartre district, offers stunning views of Paris. Montmartre itself is known for its bohemian history and is home to many artists' studios.\n\n5. **Seine River Cruise**: A boat tour on the Seine River is a great way to see many of Paris's landmarks while enjoying a relaxing boat ride.\n\n6. **Champs-Élysées**: One of the world's most famous avenues, lined with cafes, high-end shops, and the Arc de Triomphe at one end.\n\n7. **Palace of Versailles**: Located just outside Paris, the Palace of Versailles was the principal royal residence of France from 1682, under Louis XIV. Its gardens, fountains, and palace interior are a must-see.\n\n8. **Musée d'Orsay**: Housed in a former railway station, this museum is known for its extensive collection of impressionist and post-impressionist masterpieces.\n\n9. **Centre Pompidou**: A striking architectural landmark, the Centre Pompidou is a modern and contemporary art museum that houses works from the 20th and 21st centuries.\n\n10. **Le Marais**: This historic district is known for its vibrant streets, boutiques, art galleries, and historic sites like the Place des Vosges.\n\n11. **Luxembourg Gardens**: A beautiful park in the 6th arrondissement, perfect for a leisurely stroll, a picnic, or to enjoy a quiet moment in the city.\n\n12. **Catacombs of Paris**: A unique and somewhat eerie experience, the Catacombs are an underground ossuary that holds the remains of about 6 million people.\n\n13. **Père Lachaise Cemetery**: One of the world's most visited cemeteries, notable for its famous interments, including Oscar Wilde, Jim Morrison, and Édith Piaf.\n\n14. **Palais Garnier (Opera House)**: The architectural masterpiece designed by Charles Garnier is a symbol of the opulence of the Second French Empire.\n\n15. **Local Markets and Food Tours**: Paris is a food lover's paradise. Exploring local markets or joining a food tour can be a delightful way to experience the city's culinary delights.\n\nRemember, Paris is a city best explored at a leisurely pace, allowing time to soak in the atmosphere, enjoy the local cuisine, and perhaps even take a break in one of its many charming cafes. Bon voyage!"
      },
      "logprobs": null,
      "finish_reason": "stop",
      "stop_reason": null
    }
  ],
  "usage": {
    "prompt_tokens": 21,
    "total_tokens": 825,
    "completion_tokens": 804
  }
}
```




