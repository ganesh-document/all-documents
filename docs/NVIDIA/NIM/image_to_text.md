## Publisher: **meta**

## <span style="color:blue">1. Model: meta/llama-3.2-11b-vision-instruct</span>


## Model Information
The Meta Llama 3.2 Vision collection of multimodal large language models (LLMs) is a collection of pre-trained and instruction-tuned image reasoning generative models in 11B and 90B sizes (text + images in / text out). The Llama 3.2 Vision instruction-tuned models are optimized for visual recognition, image reasoning, captioning, and answering general questions about an image. The models outperform many of the available open source and closed multimodal models on common industry benchmarks. Llama 3.2 Vision models are ready for commercial use.


**Python**

```

import requests, base64

invoke_url = "https://ai.api.nvidia.com/v1/gr/meta/llama-3.2-11b-vision-instruct/chat/completions"
stream = True

with open("image.png", "rb") as f:
  image_b64 = base64.b64encode(f.read()).decode()

assert len(image_b64) < 180_000, \
  "To upload larger images, use the assets API (see docs)"
  

headers = {
  "Authorization": "Bearer $API_KEY_REQUIRED_IF_EXECUTING_OUTSIDE_NGC",
  "Accept": "text/event-stream" if stream else "application/json"
}

payload = {
  "model": 'meta/llama-3.2-11b-vision-instruct',
  "messages": [
    {
      "role": "user",
      "content": f'What is in this image? <img src="data:image/png;base64,{image_b64}" />'
    }
  ],
  "max_tokens": 512,
  "temperature": 1.00,
  "top_p": 1.00,
  "stream": stream
}

response = requests.post(invoke_url, headers=headers, json=payload)

if stream:
    for line in response.iter_lines():
        if line:
            print(line.decode("utf-8"))
else:
    print(response.json())

```

**Shell**

```
stream=true

if [ "$stream" = true ]; then
    accept_header='Accept: text/event-stream'
else
    accept_header='Accept: application/json'
fi

image_b64=$( base64 image.png )

echo '{
  "model": "meta/llama-3.2-11b-vision-instruct",
  "messages": [
    {
      "role": "user",
      "content": "What is in this image? <img src=\"data:image/png;base64,'"$image_b64"'\" />"
    }
  ],
  "max_tokens": 512,
  "temperature": 1.00,
  "top_p": 1.00,
  "stream": true
}' > payload.json

curl https://ai.api.nvidia.com/v1/gr/meta/llama-3.2-11b-vision-instruct/chat/completions \
  -H "Authorization: Bearer $API_KEY_REQUIRED_IF_EXECUTING_OUTSIDE_NGC" \
  -H "Content-Type: application/json" \
  -H "$accept_header" \
  -d @payload.json
```


**Ref Link:**
[meta/llama-3.2-11b-vision-instruct] (https://build.nvidia.com/meta/llama-3.2-11b-vision-instruct)

## Publisher: **meta**

## <span style="color:blue">2. Model: microsoft/phi-3.5-vision-instruct</span>


## Model Information
Phi-3.5-vision is a lightweight, state-of-the-art open multimodal model built upon datasets which include - synthetic data and filtered publicly available websites - with a focus on very high-quality, reasoning dense data both on text and vision. The model belongs to the Phi-3 model family, and the multimodal version comes with 128K context length (in tokens) it can support. The model underwent a rigorous enhancement process, incorporating both supervised fine-tuning and direct preference optimization to ensure precise instruction adherence and robust safety measures. This model is ready for commercial and research use.


**Loading the model locally**

```
from PIL import Image 
import requests 
from transformers import AutoModelForCausalLM 
from transformers import AutoProcessor 

model_id = "microsoft/Phi-3.5-vision-instruct" 

model = AutoModelForCausalLM.from_pretrained(model_id, device_map="cuda", trust_remote_code=True, torch_dtype="auto", _attn_implementation='flash_attention_2')

processor = AutoProcessor.from_pretrained(model_id, trust_remote_code=True, num_crops=4) 

images = []
placeholder = ""
for i in range(1,20):
    url = f"https://image.slidesharecdn.com/azureintroduction-191206101932/75/Introduction-to-Microsoft-Azure-Cloud-{i}-2048.jpg" 
    images.append(Image.open(requests.get(url, stream=True).raw))
    placeholder += f"<|image_{i}|>\n"

messages = [
    {"role": "user", "content": placeholder+"Summarize the deck of slides."},
]

prompt = processor.tokenizer.apply_chat_template(messages, tokenize=False, add_generation_prompt=True)

inputs = processor(prompt, images, return_tensors="pt").to("cuda:0") 

generation_args = { 
    "max_new_tokens": 1000, 
    "temperature": 0.0, 
    "do_sample": False, 
} 

generate_ids = model.generate(**inputs, eos_token_id=processor.tokenizer.eos_token_id, **generation_args) 

# remove input tokens 
generate_ids = generate_ids[:, inputs['input_ids'].shape[1]:]
response = processor.batch_decode(generate_ids, skip_special_tokens=True, clean_up_tokenization_spaces=False)[0] 

print(response)
```

**Python**

```

import requests, base64

invoke_url = "https://integrate.api.nvidia.com/v1/chat/completions"
stream = True


with open("dog.jpeg", "rb") as f:
  image_b64 = base64.b64encode(f.read()).decode()

assert len(image_b64) < 180_000, \
  "To upload larger images, use the assets API (see docs)"
  


headers = {
  "Authorization": "Bearer $API_KEY_REQUIRED_IF_EXECUTING_OUTSIDE_NGC",
  "Accept": "text/event-stream" if stream else "application/json"
}

payload = {
  "model": 'microsoft/phi-3.5-vision-instruct',
  "messages": [
    {
      "role": "user",
      "content": f'Describe the image. <img src="data:image/jpeg;base64,{image_b64}" />'
    }
  ],
  "max_tokens": 512,
  "temperature": 0.20,
  "top_p": 0.70,
  "stream": stream
}

response = requests.post(invoke_url, headers=headers, json=payload)

if stream:
    for line in response.iter_lines():
        if line:
            print(line.decode("utf-8"))
else:
    print(response.json())
```

**Shell**

```
stream=true

if [ "$stream" = true ]; then
    accept_header='Accept: text/event-stream'
else
    accept_header='Accept: application/json'
fi


image_b64=$( base64 dog.jpeg )

echo '{
  "model": "microsoft/phi-3.5-vision-instruct",
  "messages": [
    {
      "role": "user",
      "content": "Describe the image. <img src=\"data:image/jpeg;base64,'"$image_b64"'\" />"
    }
  ],
  "max_tokens": 512,
  "temperature": 0.20,
  "top_p": 0.70,
  "stream": true
}' > payload.json

curl https://integrate.api.nvidia.com/v1/chat/completions \
  -H "Authorization: Bearer $API_KEY_REQUIRED_IF_EXECUTING_OUTSIDE_NGC" \
  -H "Content-Type: application/json" \
  -H "$accept_header" \
  -d @payload.json

```


**Ref Link:**
[microsoft/phi-3.5-vision-instruct] (https://build.nvidia.com/microsoft/phi-3_5-vision-instruct)


## Publisher: **microsoft**

## <span style="color:blue">3. Model: microsoft/florence-2</span>


## Model Information
Florence-2 is an advanced vision foundation model using a prompt-based approach to handle a wide range of vision and vision-language tasks. It can interpret simple text prompts to perform tasks like captioning, object detection and segmentation.


**Python**

```
# The model can perform 14 different vision language model and computer vision tasks. The input ```content``` field should be formatted as ```"<TASK_PROMPT><text_prompt (only when needed)><img>"```.
# Users need to specify the task type at the beginning. Image supports both base64 and NvCF asset id. Some tasks require a text prompt, and users need to provide that after image. Below are the examples for each task.
# For <CAPTION_TO_PHRASE_GROUNDING>, <REFERRING_EXPRESSION_SEGMENTATION>, <OPEN_VOCABULARY_DETECTION>, users can change the text prompt as other descriptions.
# For <REGION_TO_SEGMENTATION>, <REGION_TO_CATEGORY>, <REGION_TO_DESCRIPTION>, the text prompt is formatted as <loc_x1><loc_y1><loc_x2><loc_y2>, which is the normalized coordinates from region of interest bbox. x1=int(top_left_x_coor/width*999), y1=int(top_left_y_coor/height*999), x2=int(bottom_right_x_coor/width*999), y2=int(bottom_right_y_coor/height*999).
import os
import sys
import zipfile
import requests

nvai_url = "https://ai.api.nvidia.com/v1/vlm/microsoft/florence-2"
header_auth = f'Bearer {os.getenv("API_KEY_REQUIRED_IF_EXECUTING_OUTSIDE_NGC", "")}'
prompts = ["<CAPTION>",
    "<DETAILED_CAPTION>",
    "<MORE_DETAILED_CAPTION>",
    "<OD>",
    "<DENSE_REGION_CAPTION>",
    "<REGION_PROPOSAL>",
    "<CAPTION_TO_PHRASE_GROUNDING>A black and brown dog is laying on a grass field.",
    "<REFERRING_EXPRESSION_SEGMENTATION>a black and brown dog",
    "<REGION_TO_SEGMENTATION><loc_312><loc_168><loc_998><loc_846>",
    "<OPEN_VOCABULARY_DETECTION>a black and brown dog",
    "<REGION_TO_CATEGORY><loc_312><loc_168><loc_998><loc_846>",
    "<REGION_TO_DESCRIPTION><loc_312><loc_168><loc_998><loc_846>",
    "<OCR>",
    "<OCR_WITH_REGION>"]


def _upload_asset(input, description):
    """
    Uploads an asset to the NVCF API.
    :param input: The binary asset to upload
    :param description: A description of the asset

    """

    authorize = requests.post(
        "https://api.nvcf.nvidia.com/v2/nvcf/assets",
        headers={
            "Authorization": header_auth,
            "Content-Type": "application/json",
            "accept": "application/json",
        },
        json={"contentType": "image/jpeg", "description": description},
        timeout=30,
    )
    authorize.raise_for_status()

    response = requests.put(
        authorize.json()["uploadUrl"],
        data=input,
        headers={
            "x-amz-meta-nvcf-asset-description": description,
            "content-type": "image/jpeg",
        },
        timeout=300,
    )

    response.raise_for_status()
    return str(authorize.json()["assetId"])

def _generate_content(task_id, asset_id):
    if task_id < 0 or task_id >= len(prompts):
        print(f"task_id should within [0, {len(prompts)-1}]")
        exit(1)
    prompt = prompts[task_id]
    content = f'{prompt}<img src="data:image/jpeg;asset_id,{asset_id}" />'
    return content

if __name__ == "__main__":
    """Uploads two images of your choosing to the NVCF API and sends a request
    to the Visual ChangeNet model to compare them. The response is saved to
    <output_dir>
    """

    if len(sys.argv) != 4:
        print("Usage: python test.py <test_image> <result_dir> <task_id>\n"
            "For example: python test.py car.jpg result_dir 0")
        sys.exit(1)

    if len(os.getenv("API_KEY_REQUIRED_IF_EXECUTING_OUTSIDE_NGC", "")) == 0:
        print("API_KEY not set. Please export API_KEY_REQUIRED_IF_EXECUTING_OUTSIDE_NGC=<Your API Key> as environment variable.")
        sys.exit(1)

    # Local images
    asset_id = _upload_asset(open(sys.argv[1], "rb"), "Test Image")
    content = _generate_content(int(sys.argv[3]), asset_id)
    # Asset IDs returned by the _upload_asset function
    inputs = {
        "messages": [{
            "role": "user",
            "content": content
        }]
    }
    # asset_list = f"{asset_id}"
    headers = {
        "Content-Type": "application/json",
        "NVCF-INPUT-ASSET-REFERENCES": asset_id,
        "NVCF-FUNCTION-ASSET-IDS": asset_id,
        "Authorization": header_auth,
        "Accept": "application/json"
    }

    print(asset_id, inputs)

    # Send the request to the NIM API.
    response = requests.post(nvai_url, headers=headers, json=inputs)

    with open(f"{sys.argv[2]}.zip", "wb") as out:
        out.write(response.content)

    with zipfile.ZipFile(f"{sys.argv[2]}.zip", "r") as z:
        z.extractall(sys.argv[2])

    print(f"Response saved to path: {sys.argv[2]}. File list: {os.listdir(sys.argv[2])}")
```

**Shell**

```
#!/bin/bash
# The model can perform 14 different vision language model and computer vision tasks. The input ```content``` field should be formatted as ```"<TASK_PROMPT><text_prompt (only when needed)><img>"```.
# Users need to specify the task type at the beginning. Image supports both base64 and NvCF asset id. Some tasks require a text prompt, and users need to provide that after image. Below are the examples for each task.
# For <CAPTION_TO_PHRASE_GROUNDING>, <REFERRING_EXPRESSION_SEGMENTATION>, <OPEN_VOCABULARY_DETECTION>, users can change the text prompt as other descriptions.
# For <REGION_TO_SEGMENTATION>, <REGION_TO_CATEGORY>, <REGION_TO_DESCRIPTION>, the text prompt is formatted as <loc_x1><loc_y1><loc_x2><loc_y2>, which is the normalized coordinates from region of interest bbox. x1=int(top_left_x_coor/width*999), y1=int(top_left_y_coor/height*999), x2=int(bottom_right_x_coor/width*999), y2=int(bottom_right_y_coor/height*999).

set -e

# Check arguments
if [ "$#" -ne 3 ]; then
    printf "Usage: ./test.sh <test_image> <result_dir> <task_id>\nFor example: ./test.sh car.jpg result_dir 0\n"
    exit 1
fi

if [[ -z "${API_KEY_REQUIRED_IF_EXECUTING_OUTSIDE_NGC}" ]]; then
    echo "API_KEY not set. Please export API_KEY_REQUIRED_IF_EXECUTING_OUTSIDE_NGC=<Your API Key> as environment variable."
    exit 1

fi
# Set variables
nvai_url="https://ai.api.nvidia.com/v1/vlm/microsoft/florence-2"
api_key=$API_KEY_REQUIRED_IF_EXECUTING_OUTSIDE_NGC
assets_url="https://api.nvcf.nvidia.com/v2/nvcf/assets"

prompts=(
    "<CAPTION>"
    "<DETAILED_CAPTION>"
    "<MORE_DETAILED_CAPTION>"
    "<OD>"
    "<DENSE_REGION_CAPTION>"
    "<REGION_PROPOSAL>"
    "<CAPTION_TO_PHRASE_GROUNDING>A black and brown dog is laying on a grass field."
    "<REFERRING_EXPRESSION_SEGMENTATION>a black and brown dog"
    "<REGION_TO_SEGMENTATION><loc_312><loc_168><loc_998><loc_846>"
    "<OPEN_VOCABULARY_DETECTION>a black and brown dog"
    "<REGION_TO_CATEGORY><loc_312><loc_168><loc_998><loc_846>"
    "<REGION_TO_DESCRIPTION><loc_312><loc_168><loc_998><loc_846>"
    "<OCR>"
    "<OCR_WITH_REGION>"
)

content_type="image/jpeg"
description="Test Image"

# Function to upload an asset
upload_asset() {
    local input=$1
    local description=$2

    # Authorize upload
    authorize=$(curl -s -X POST $assets_url \
        -H "Authorization: Bearer $api_key" \
        -H "Content-Type: application/json" \
        -H "accept: application/json" \
        -d "{\"contentType\": \"$content_type\", \"description\": \"$description\"}")

    # Get upload URL and asset ID
    upload_url=$(echo $authorize | jq -r '.uploadUrl')
    asset_id=$(echo $authorize | jq -r '.assetId')

    # Upload asset
    curl -s -X PUT $upload_url \
        -H "x-amz-meta-nvcf-asset-description: $description" \
        -H "content-type: $content_type" \
        --upload-file $input

    echo $asset_id
}

# Function to generate content
generate_content() {
    local task_id=$1
    local asset_id=$2
    prompt=${prompts[$task_id]}
    content="$prompt<img src=\\\"data:image/jpeg;asset_id,$asset_id\\\" />"

    echo $content
}

# Upload images
asset_id=$(upload_asset $1 $description)
content=$(generate_content $3 $asset_id)
echo '{
    "messages":[{
        "role": "user",
        "content": "'"$content"'"
        }]
    }' > payload.json

mkdir -p $2
# Compare images via microservice
location_command="curl -D - -s -X POST $nvai_url \
  -H \"Content-Type: application/json\" \
  -H \"NVCF-INPUT-ASSET-REFERENCES: $asset_id\" \
  -H \"NVCF-FUNCTION-ASSET-IDS: $asset_id\" \
  -H \"Authorization: Bearer $api_key\" \
  -d @payload.json \
  | grep location | awk '{print \$2}'"

location=$(eval ${location_command} | tr -d '\n' | tr -d '\r' | tr -d ' ' | tr -d '"' | tr -d ',')

# The download command will download the file from the location header
download_command="curl -s '${location}' > $2.zip"
echo $location_command

# Download the .zip file
response=$(eval ${download_command})

# Unzip the file
unzip -q $2.zip -d $2

echo "Response saved to $2.zip"
echo $(ls $2)
```

**Ref Link:**
[microsoft/florence-2] (https://build.nvidia.com/microsoft/microsoft-florence-2)

## Publisher: **google**

## <span style="color:blue">4. Model: google/paligemma</span>


## Model Information
The Google PaLIGemma-3B-mix model is a one-shot visual language understanding solution for image-to-text generation. This model is ready for commercial use.

**Python**

```

import requests, base64

invoke_url = "https://ai.api.nvidia.com/v1/vlm/google/paligemma"
stream = True

with open("dog.jpeg", "rb") as f:
    image_b64 = base64.b64encode(f.read()).decode()

assert len(image_b64) < 180_000, \
  "To upload larger images, use the assets API (see docs)"

headers = {
  "Authorization": "Bearer $API_KEY_REQUIRED_IF_EXECUTING_OUTSIDE_NGC",
  "Accept": "text/event-stream" if stream else "application/json"
}

payload = {
  "messages": [
    {
      "role": "user",
      "content": f'Describe the image. <img src="data:image/jpeg;base64,{image_b64}" />'
    }
  ],
  "max_tokens": 512,
  "temperature": 1.00,
  "top_p": 0.70,
  "stream": stream
}

response = requests.post(invoke_url, headers=headers, json=payload)

if stream:
    for line in response.iter_lines():
        if line:
            print(line.decode("utf-8"))
else:
    print(response.json())
```

**Shell**

```
image_b64=$( base64 dog.jpeg )
stream=true

if [ "$stream" = true ]; then
    accept_header='Accept: text/event-stream'
else
    accept_header='Accept: application/json'
fi

echo '{
  "messages": [
    {
      "role": "user",
      "content": "Describe the image. <img src=\"data:image/jpeg;base64,'"$image_b64"'\" />"
    }
  ],
  "max_tokens": 512,
  "temperature": 1.00,
  "top_p": 0.70,
  "stream": true
}' > payload.json

curl https://ai.api.nvidia.com/v1/vlm/google/paligemma \
  -H "Authorization: Bearer $API_KEY_REQUIRED_IF_EXECUTING_OUTSIDE_NGC" \
  -H "Content-Type: application/json" \
  -H "$accept_header" \
  -d @payload.json
```

**Ref Link:**
[google/paligemma] (https://build.nvidia.com/google/google-paligemma)


## Publisher: **nvidia**

## <span style="color:blue">4. Model: nvidia/neva-22b</span>


## Model Information
NeVA is NVIDIA's version of the LLaVA model where the open source LLaMA model is replaced with a GPT model trained by NVIDIA. At a high level the image is encoded using a frozen hugging face CLIP model and projected to the text embedding dimensions. This is then concatenated with the embeddings of the prompt and passed in through the language model. Training happens in two stages:

Pretraining: Here the language model is frozen and only the projection layer (that maps the image encoding to the embedding space) is trained. Here, image-caption pairs are used to pretrain the model.
Finetuning: Here the language model is also trained along with the projection layer. To finetune the model synthetic instruction data generated using GPT4 is used.

**Python**

```

import requests, base64

invoke_url = "https://ai.api.nvidia.com/v1/vlm/nvidia/neva-22b"
stream = True

with open("dog.png", "rb") as f:
    image_b64 = base64.b64encode(f.read()).decode()

assert len(image_b64) < 180_000, \
  "To upload larger images, use the assets API (see docs)"

headers = {
  "Authorization": "Bearer $API_KEY_REQUIRED_IF_EXECUTING_OUTSIDE_NGC",
  "Accept": "text/event-stream" if stream else "application/json"
}

payload = {
  "messages": [
    {
      "role": "user",
      "content": f'Describe what you see in this image. <img src="data:image/png;base64,{image_b64}" />'
    }
  ],
  "max_tokens": 1024,
  "temperature": 0.20,
  "top_p": 0.70,
  "seed": 0,
  "stream": stream
}

response = requests.post(invoke_url, headers=headers, json=payload)

if stream:
    for line in response.iter_lines():
        if line:
            print(line.decode("utf-8"))
else:
    print(response.json())
```

**Shell**

```
image_b64=$( base64 dog.png )
stream=true

if [ "$stream" = true ]; then
    accept_header='Accept: text/event-stream'
else
    accept_header='Accept: application/json'
fi

echo '{
  "messages": [
    {
      "role": "user",
      "content": "Describe what you see in this image. <img src=\"data:image/png;base64,'"$image_b64"'\" />"
    }
  ],
  "max_tokens": 1024,
  "temperature": 0.20,
  "top_p": 0.70,
  "seed": 0,
  "stream": true
}' > payload.json

curl https://ai.api.nvidia.com/v1/vlm/nvidia/neva-22b \
  -H "Authorization: Bearer $API_KEY_REQUIRED_IF_EXECUTING_OUTSIDE_NGC" \
  -H "Content-Type: application/json" \
  -H "$accept_header" \
  -d @payload.json
```


**Ref Link:**
[nvidia/neva-22b] (https://build.nvidia.com/google/google-paligemma)


## Publisher: **microsoft**

## <span style="color:blue">5. Model: microsoft/kosmos-2</span>


## Model Information
Kosmos-2 model is a groundbreaking multimodal large language model (MLLM). Kosmos-2 is designed to ground text to the visual world, enabling it to understand and reason about visual elements in images.

**Python**

```
import requests, base64

invoke_url = "https://ai.api.nvidia.com/v1/vlm/microsoft/kosmos-2"

with open("soccer.png", "rb") as f:
    image_b64 = base64.b64encode(f.read()).decode()

assert len(image_b64) < 180_000, \
  "To upload larger images, use the assets API (see docs)"

headers = {
  "Authorization": "Bearer $API_KEY_REQUIRED_IF_EXECUTING_OUTSIDE_NGC",
  "Accept": "application/json"
}

payload = {
  "messages": [
    {
      "role": "user",
      "content": f'Who is in this photo? <img src="data:image/png;base64,{image_b64}" />'
    }
  ],
  "max_tokens": 1024,
  "temperature": 0.20,
  "top_p": 0.20
}

response = requests.post(invoke_url, headers=headers, json=payload)

print(response.json())
```

**Shell**

```
image_b64=$( base64 soccer.png )

echo '{
  "messages": [
    {
      "role": "user",
      "content": "Who is in this photo? <img src=\"data:image/png;base64,'"$image_b64"'\" />"
    }
  ],
  "max_tokens": 1024,
  "temperature": 0.20,
  "top_p": 0.20
}' > payload.json

curl https://ai.api.nvidia.com/v1/vlm/microsoft/kosmos-2 \
  -H "Authorization: Bearer $API_KEY_REQUIRED_IF_EXECUTING_OUTSIDE_NGC" \
  -H "Content-Type: application/json" \
  -H "Accept: application/json" \
  -d @payload.json
```

**Ref Link:**
[microsoft/kosmos-2] (https://build.nvidia.com/microsoft/microsoft-kosmos-2)


## Publisher: **google**

## <span style="color:blue">6. Model: google/deplot</span>


## Model Information
The Google DePlot model is a one-shot visual language understanding solution that translates images of plots or charts into linearized tables.

**Python**

```

import requests, base64

invoke_url = "https://ai.api.nvidia.com/v1/vlm/google/deplot"
stream = True

with open("economic-assistance-chart.png", "rb") as f:
    image_b64 = base64.b64encode(f.read()).decode()

assert len(image_b64) < 180_000, \
  "To upload larger images, use the assets API (see docs)"

headers = {
  "Authorization": "Bearer $API_KEY_REQUIRED_IF_EXECUTING_OUTSIDE_NGC",
  "Accept": "text/event-stream" if stream else "application/json"
}

payload = {
  "messages": [
    {
      "role": "user",
      "content": f'Generate underlying data table of the figure below: <img src="data:image/png;base64,{image_b64}" />'
    }
  ],
  "max_tokens": 1024,
  "temperature": 0.20,
  "top_p": 0.20,
  "stream": stream
}

response = requests.post(invoke_url, headers=headers, json=payload)

if stream:
    for line in response.iter_lines():
        if line:
            print(line.decode("utf-8"))
else:
    print(response.json())
```

**Shell**

```
image_b64=$( base64 economic-assistance-chart.png )
stream=true

if [ "$stream" = true ]; then
    accept_header='Accept: text/event-stream'
else
    accept_header='Accept: application/json'
fi

echo '{
  "messages": [
    {
      "role": "user",
      "content": "Generate underlying data table of the figure below: <img src=\"data:image/png;base64,'"$image_b64"'\" />"
    }
  ],
  "max_tokens": 1024,
  "temperature": 0.20,
  "top_p": 0.20,
  "stream": true
}' > payload.json

curl https://ai.api.nvidia.com/v1/vlm/google/deplot \
  -H "Authorization: Bearer $API_KEY_REQUIRED_IF_EXECUTING_OUTSIDE_NGC" \
  -H "Content-Type: application/json" \
  -H "$accept_header" \
  -d @payload.json
```


**Ref Link:**
[google/deplot] (https://build.nvidia.com/google/google-deplot)

