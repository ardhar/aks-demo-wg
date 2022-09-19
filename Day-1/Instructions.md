
# **How to Dockerize an Aplication**
### Important files
1. app.py
2. Dockerfile
3. app.yaml
4. requirements.txt

### System Requirement
1. Create a VM running Linux - Ubuntu 18.04 or 20.XX
2. Ensure you are able to SSH
3. Install Docker
3. Install kubectl command line tool to manage Kubernetes


# Buidling an Image
<i> docker build -t image_name:tag . </i>

# Command to check if the image is created
<i> docker image ls </i>

# Running container from the image
<i> docker container run -p 8080:5001 [docker_image] </i>

# Pushing the Image to Azure Container Registry
<i> docker tag apptest1:latest <acr_name>.azurecr.io/image:tag </i> <br>
<i> docker push <acr_name>.azurecr.io/image:tag </i>

# Deploying the application on AKS Cluster
<i> kubectl create -f app.yaml </i>
