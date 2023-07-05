# Google Cloud ARM64 VMs

These were created with these settings:

```sh
gcloud compute instances create INSTANCE_NAME_HERE \
    --project=GCLOUD_PROJECT_NAME_HERE \
    --zone=us-central1-f \
    --machine-type=t2a-standard-4 \
    --create-disk=auto-delete=yes,boot=yes,image=projects/ubuntu-os-cloud/global/images/ubuntu-2204-jammy-arm64-v20230908,mode=rw,size=50
```
