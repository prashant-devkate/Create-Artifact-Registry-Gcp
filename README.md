## Creating an Artifact Registry in Google Cloud to deploy Docker Containers

### Step 1: Open Artifact Registry
1. Go to the [Google Cloud Console](https://console.cloud.google.com/).
2. In the **Navigation menu** (☰), go to **Artifact Registry**.
3. Click **Create Repository**.

### Step 2: Configure the Repository
1. **Repository Name**: `gcp-deployment`
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

#### Example Usage
After running the command, image can be pushed to Artifact Registry:

```
sh docker push us-central1-docker.pkg.dev/MY_PROJECT_ID/MY_REPOSITORY/MY_IMAGE:latest
```
