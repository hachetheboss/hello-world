# Hello World Applications

This repository contains Hello World applications in Python and Java, along with containerization and deployment configurations for ROSA (Red Hat OpenShift Service on AWS).

## Local Development

### Prerequisites
- Docker and Docker Compose
- Java 21 (for local development)
- Python 3.11
- OpenShift CLI (oc)

### Running Locally with Docker Compose
```bash
docker-compose up --build
```

Access the applications at:
- Python: http://localhost:5000
- Java: http://localhost:5001

## Deploying to ROSA

1. Log in to your ROSA cluster:
```bash
oc login --token=<your-token> --server=<your-cluster-api>
```

2. Create a new project:
```bash
oc new-project hello-world
```

3. Build and push images to your container registry:
```bash
# Update image references in k8s/*.yml files with your registry path
docker build -t <your-registry>/hello-world-python:latest python/
docker build -t <your-registry>/hello-world-java:latest java/
docker push <your-registry>/hello-world-python:latest
docker push <your-registry>/hello-world-java:latest
```

4. Deploy to ROSA:
```bash
oc apply -f k8s/python-deployment.yml
oc apply -f k8s/java-deployment.yml
```

5. Get the routes:
```bash
oc get routes
``` 
