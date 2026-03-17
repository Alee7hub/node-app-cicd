# Node.js CI/CD Pipeline with Jenkins & Docker

A Node.js/Express web application with a fully automated CI/CD pipeline built with Jenkins. The pipeline handles semantic versioning, automated testing, Docker image builds, and publishing — end to end, without manual intervention.

## Stack

- **App**: Node.js + Express
- **CI/CD**: Jenkins (Declarative Pipeline + Shared Library)
- **Containerization**: Docker (published to Docker Hub)
- **Testing**: Jest

## Pipeline Stages

1. **Increment Version** — Auto-bumps the minor version in `package.json` using semantic versioning
2. **Test** — Runs the Jest test suite
3. **Build Docker Image** — Builds a versioned Docker image from the `Dockerfile`
4. **Push Docker Image** — Authenticates and pushes the image to Docker Hub
5. **Commit Version Bump** — Commits and pushes the updated `package.json` back to GitHub via Jenkins

The pipeline is backed by a **Jenkins Shared Library** (`sl-node-app-cicd`), keeping the Jenkinsfile clean and the pipeline logic reusable across projects.

## Running Locally

```bash
cd app
npm install
npm start          # starts on http://localhost:3000
```

## Running Tests

```bash
cd app
npm install
npm run test
```

## Docker

```bash
docker build -t node-app-cicd .
docker run -p 3000:3000 node-app-cicd
```