## Publisher: **nvidia**

## <span style="color:blue">1. Model: nvidia/maisi</span>


## Model Information
NVIDIA MAISI (Medical AI for Synthetic Imaging) is a state-of-the-art three-dimensional (3D) Latent Diffusion Model designed for generating high-quality synthetic CT images with or without anatomical annotations. This AI model excels in data augmentation and creating realistic medical imaging data to supplement limited datasets due to privacy concerns or rare conditions. It can also significantly enhance the performance of other medical imaging AI models by generating diverse and realistic training data.

**Python**

```
import io
import os
import time
import requests
import shutil
import tempfile
import zipfile

invoke_url = "https://health.api.nvidia.com/v1/medicalimaging/nvidia/maisi"
fetch_url="https://api.nvcf.nvidia.com/v2/nvcf/pexec/status/"
headers = {
    "Authorization": "Bearer $API_KEY_REQUIRED_IF_EXECUTING_OUTSIDE_NGC",
    "Accept": "application/json",
    "content_type_header": "Content-Type: application/json"
}

result = "result-1"
payload = {
    "num_output_samples": 1,
    "body_region": ["chest"],
    "anatomy_list": ["liver"],
    "controllable_anatomy_size": [["hepatic tumor", 0.3], ["liver", 0.5]],
    "output_size": [512, 512, 512],
    "image_output_ext": ".nii.gz",
    "label_output_ext": ".nii.gz",
    "pre_signed_url": "",
    "spacing": [1, 1, 1],
}

# re-use connections
session = requests.Session()
response = session.post(invoke_url, headers=headers, json=payload)

response.raise_for_status()
while response.status_code == 202:
    req_id = response.headers.get("NVCF-REQID")
    req_url = os.path.join(fetch_url, req_id)
    response = session.get(req_url, headers=headers)
    print(f"Please wait util response returned...")
    time.sleep(1)

if response.status_code != 200:
    print(f"Error with code {response.status_code}.")
    exit()

with tempfile.TemporaryDirectory() as temp_dir:
    z = zipfile.ZipFile(io.BytesIO(response.content))
    z.extractall(temp_dir)
    os.makedirs(result)
    shutil.move(temp_dir, f"{result}")

print("Success!")
```

**Shell**

```
invoke_url="https://health.api.nvidia.com/v1/medicalimaging/nvidia/maisi"
authorization_header="Authorization: Bearer $API_KEY_REQUIRED_IF_EXECUTING_OUTSIDE_NGC"
content_type_header="Content-Type: application/json"
accept_header="Accept: application/json"
FETCH_URL="https://api.nvcf.nvidia.com/v2/nvcf/pexec/status/"

OUTPUT_DIR="result-1"
data='{
    "num_output_samples": 1,
    "body_region": ["chest"],
    "anatomy_list": ["liver"],
    "output_size": [512, 512, 512],
    "controllable_anatomy_size": [["hepatic tumor", 0.3], ["liver", 0.5]],
    "image_output_ext": ".nii.gz",
    "label_output_ext": ".nii.gz",
    "pre_signed_url": "",
    "spacing": [1, 1, 1]
}'


echo "Invoking the MAISI microservice..."
response=$(curl --silent -i --request POST --url "$invoke_url" \
  --header "$authorization_header" \
  --header "$content_type_header" \
  --header "$accept_header"      \
  --data "$data")

status_code=$(echo "$response" | head -n 1 | awk '{print $2}')
if [ $status_code = "202" ]; then
    echo "Request accepted. Fetching the output..."
    req_id=$(echo "$response" | grep -i '^nvcf-reqid:' | awk '{print $2}' | tr -d '\r')
    while true; do
        response=$(curl -s -L -o output.zip -w "%{http_code}" -H "$content_type_header" -H "$authorization_header" -H "$accept_header" "${FETCH_URL}${req_id}")

        if [ "$response" -eq 200 ]; then
            echo "Download of output zip file is complete."
            break
        else
            echo "Please waiting until response returned..."
            sleep 1
        fi
    done
    unzip output.zip -d $OUTPUT_DIR && rm output.zip && rm $OUTPUT_DIR/*.response
elif [ $status_code = "302" ]; then
    location=$(echo "$response" | grep -i '^location:' | awk '{print $2}' | tr -d '\r')
    echo "Redirecting url..."
    curl -s -o output.zip -H "$accept_header" $location
    unzip output.zip -d $OUTPUT_DIR && rm output.zip && rm $OUTPUT_DIR/*.response
else
    echo "Error Response: $response"
fi
```

**Ref Link:**
[nvidia/maisi] (https://build.nvidia.com/nvidia/maisi)

