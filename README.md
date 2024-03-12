# SampleMERNwithMicroservices
# MERN_App_Microservices_GCP
## Objective:
### Deploying a MERN Microservice Application using Kubernetes in GCP.

Prerequisites
1: Launch a GCP VM.

2: Install gcloud CLI in it

Follow the link https://cloud.google.com/sdk/docs/install#deb to install gcloud cli for your desired OS.

3: Install docker in it

4: Install Kubectl in it

Set Up the gcloud CLI
1: To initialize the gcloud CLI, run
```
gcloud init
```
2: Create or select a configuration if prompted.

If you are initializing a new gcloud CLI installation, gcloud init creates a configuration named default for you and sets it as the active configuration. If you have existing configurations, gcloud init prompts you to choose between three options — re-initialize the active one, switch to another one and re-initialize it, or create a new one.
3: Choose a current Google Cloud project if prompted.
```
This account has a lot of projects! Listing them all can take a while.
 [1] Enter a project ID
 [2] Create a new project
 [3] List projects
Please enter your numeric choice:
```
4: Run gcloud auth login
```
gcloud auth login
```
Prepare the MERN Application
Containerize the MERN Application:

Ensure the MERN application is containerized using Docker. Create a Dockerfile for each component (frontend and backend).
Docker Images:

Establish a connect between Docker and GCP using the following command.
```
gcloud auth configure-docker YOUR-REGION-docker.pkg.dev
```
Build Docker images for the frontend and backend.
```
docker build -t frontendmern
docker build -t profilebackendmern .
docker build -t hellobackendmern .
```
Create repositories in Artifact registory
![image](https://github.com/rk630/Mern_Application_GKE/assets/139606316/8d1abde9-c926-400e-8d2c-1c51de722b84)

Now lets tag and push the Docker images to GCP Artifact Registry.
Hello Service:
```
docker tag frontendmern asia-southeast1-docker.pkg.dev/gke-orchestration/frontend/frontend
```
To push
```
docker push asia-southeast1-docker.pkg.dev/gke-orchestration/frontend/frontend
```
![image](https://github.com/rk630/Mern_Application_GKE/assets/139606316/55649c37-2563-4a5d-bdaa-e3557b307a0a)
![image](https://github.com/rk630/Mern_Application_GKE/assets/139606316/409f6d7b-5092-4337-b81a-2e26eab55fbe)
![image](https://github.com/rk630/Mern_Application_GKE/assets/139606316/8c1c3dbf-c525-4f30-91a8-a2fb0e451c2a)

### Kubernetes (GKE) Deployment
1. Create GKE Cluster:
   ```
   gcloud container clusters create mern-app --min-nodes=1 --num-nodes=2 --max-nodes=3 --zone=asia-south1-a --machine-type e2-small
   ```
   ![image](https://github.com/rk630/Mern_Application_GKE/assets/139606316/1001ecaa-050b-4c13-bee9-f3041986b3dd)

2. Pass the env variables into the deployment.yaml file and by using the below command create a mongo secret to store in gcp
```
kubectl create secret generic mongo-secret --from-literal=MONGO_URL=" your mongo db url"
```
![image](https://github.com/rk630/Mern_Application_GKE/assets/139606316/ca5feb57-7dc0-4776-8775-e1ebaddb433b)

3. Apply all the deployment.yaml files from the following link using the below command
   ```
   kubectl apply -f <deployment-file-name.yml>
   ```
   ![image](https://github.com/rk630/Mern_Application_GKE/assets/139606316/c3513182-843a-4f72-9276-ac09e85c14da)

![image](https://github.com/rk630/Mern_Application_GKE/assets/139606316/f206951b-1bd3-4793-9fdc-c038ad89928b)
![Screenshot 2024-01-08 204006](https://github.com/rk630/Mern_Application_GKE/assets/139606316/29f08771-32de-4acf-bbd2-bbef413b27b5)


