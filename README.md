# CI/CD Pipeline — Flask + Docker + Kubernetes

A complete CI/CD pipeline project built for learning DevOps.

## What this does

Every `git push` to `main` automatically:
1. Runs tests
2. Builds a Docker image
3. Pushes the image to DockerHub
4. Deploys to a Kubernetes (kind) cluster

## Tech Stack

- **App**: Python Flask
- **Containerization**: Docker
- **CI/CD**: GitHub Actions
- **Orchestration**: Kubernetes (kind)
- **Registry**: DockerHub

## Project Structure

```
my-cicd-project/
├── app.py                          # Flask web app
├── requirements.txt                # Python dependencies
├── Dockerfile                      # Container build instructions
├── k8s/
│   ├── deployment.yaml             # K8s Deployment manifest
│   └── service.yaml                # K8s Service manifest
├── tests/
│   └── test_app.py                 # Unit tests
└── .github/
    └── workflows/
        └── pipeline.yml            # GitHub Actions workflow
```

## Setup

### 1. Fork & clone this repo

```bash
git clone https://github.com/YOUR_USERNAME/my-cicd-project.git
cd my-cicd-project
```

### 2. Add GitHub Secrets

Go to your repo → Settings → Secrets and variables → Actions:

| Secret | Value |
|--------|-------|
| `DOCKER_USERNAME` | Your DockerHub username |
| `DOCKER_PASSWORD` | Your DockerHub password or access token |

### 3. Update the image name

In `k8s/deployment.yaml`, replace:
```
image: YOUR_DOCKERHUB_USERNAME/flask-cicd:latest
```
with your actual DockerHub username.

### 4. Push to trigger the pipeline

```bash
git add .
git commit -m "initial commit"
git push origin main
```

Watch the pipeline run in the **Actions** tab on GitHub.

## Run locally

```bash
pip install -r requirements.txt
python app.py
# visit http://localhost:5000
```

## Run tests locally

```bash
pytest tests/ -v
```

## Run with Docker locally

```bash
docker build -t flask-cicd .
docker run -p 5000:5000 flask-cicd
# visit http://localhost:5000
```
