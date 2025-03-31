## Creating an Artifact Registry in Google Cloud to deploy Docker Containers

### Step 1: Open Artifact Registry
1. Go to the [Google Cloud Console](https://console.cloud.google.com/).
2. In the **Navigation menu** (☰), go to **Artifact Registry**.
3. Click **Create Repository**.

### Step 2: Configure the Repository
1. **Repository Name**: `cloudrun-app`
2. **Format**: **Docker**
3. **Region**: `us-central1`
4. **Encryption**: **Google-managed encryption key**

### Step 3: Create the Repository
Click **Create**.

### Step 4: Authenticate Docker to Push Images
After creation, need to authenticate Docker to push images:

Run this in terminal (PowerShell or Command Prompt):

```sh
gcloud auth configure-docker us-central1-docker.pkg.dev
```

#### What Happens When You Run This Command?
 🔹 **`configure-docker`** → Configures Docker to use Google Cloud authentication for pushing/pulling images.
 🔹 **`us-central1-docker.pkg.dev`** → The Artifact Registry domain(`pkg.dev`) for the us-central1 region.

### Step 5: Tagging the Docker Image

```sh
docker tag gcp-deployment:latest us-central1-docker.pkg.dev/my-cloud-project-id/cloudrun-app/gcp-deployment:latest
```

- **`docker tag`** → Tags an existing image with a new name.
- **`gcp-deployment:latest`** → **existing local image**.
- **`us-central1-docker.pkg.dev/my-cloud-project-id/cloudrun-app/gcp-deployment:latest`** → **new name** (target location in Artifact Registry).

### Step 6: Push the Tagged Image to Artifact Registry
After tagging, you can push the image to **Artifact Registry** with:

```sh
docker push us-central1-docker.pkg.dev/my-cloud-project-id/cloudrun-app/gcp-deployment:latest
```

🔹 my-cloud-project-id > gcp project (braided-trees-453709-c4)
🔹 cloudrun-app > my artifact registry repo
🔹 gcp-deployment:latest > Docker image

![image](https://github.com/user-attachments/assets/7528b28a-dd86-4337-82d0-4628ad6042b8)

## Successfully Pushed Docker Image to Artifact Registry!

### ✅ Verify the Image in Google Cloud Console
 [Google Cloud Console](https://console.cloud.google.com/). → **Artifact Registry** → **cloudrun-app** → **`gcp-deployment:latest`** should be listed.
 
## 🛠️ Deploying the Image to Cloud Run
Now that image is stored in Artifact Registry, it can be deployed to **Google Cloud Run**:

```sh
gcloud run deploy cloudrun-app --image=us-central1-docker.pkg.dev/braided-trees-453709-c4/cloudrun-app/gcp-deployment:latest --region=us-central1 --platform=managed --allow-unauthenticated
```

### 🔍 Breakdown of the Deployment Command:
- **`gcloud run deploy cloudrun-app`** → Deploys a new **Cloud Run** service named `cloudrun-app`.
- **`--image=us-central1-docker.pkg.dev/...`** → container image to be deployed.
- **`--platform=managed`** → Uses Google’s fully managed Cloud Run service.
- **`--allow-unauthenticated`** → Allows public access to the deployed service (optional).

  **Check Deployment Status:** → using **service URL**

🎯 **containerized application is now live on Google Cloud Run!**


