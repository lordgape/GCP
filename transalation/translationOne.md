# Objectives
In this lab, you will learn how to perform the following tasks:

- Create two Compute Engine virtual machines using the gcloud command-line interface.

- Connect between the two instances.

### Steps

1. You will need google's cloud sdk install on your local machine to run cloud commands from CLI. 
- See <a href="https://cloud.google.com/sdk/docs/downloads-versioned-archives">Download and Install Google cloud sdk</a>  

2. Let create the first virtual instance called ``` my-vm-1 ``` in ```us-central1-a``` zone

```
  gcloud config set compute/zone us-central1-a
``` 

``` gcloud compute instances create "my-vm-1" --machine-type "n1-standard-1" \
--image-project "debian-cloud" \
--image "debian-9-stretch-v20190213" \
--subnet "default" --tags "http" ```


gcloud compute firewall-rules \
create allow-http --action=ALLOW --destination=INGRESS \
--rules=http:80 --target-tags=http
