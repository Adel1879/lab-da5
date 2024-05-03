+++
title = "Welcome to the DevOps Lab"
date = 2024-05-03T21:02:57+05:30
draft = false
+++

## Activity 1: Introduction to Docker

In this lab, we will look at some basic Docker commands and a simple build-ship-run workflow. We’ll start by running some simple containers, then we’ll use a Dockerfile to build a custom app. Finally, we’ll look at how to use bind mounts to modify a running container as you might if you were actively developing using Docker.

### Tasks:

- **Task 0: Prerequisites**
  Ensure you have Docker installed on your machine.

- **Task 1: Run some simple Docker containers**
  Start by running some pre-built Docker containers to get familiar with basic Docker commands.

- **Task 2: Package and run a custom app using Docker**
  Create a Dockerfile for a custom application, build it into a Docker image, and run it as a container.

- **Task 3: Modify a Running Website**
  Explore how to modify a running website using bind mounts.

### Video Explanation:
[Watch the video explanation here](LINK_OF_VIDEO_EXPLANATION)

### Implementation Guide:
[Access the Google Doc with detailed implementation steps](LINK_OF_GOOGLE_DOC_OF_IMPLEMENTATION)

---

## Activity 2: Setting up Minikube as a CI Step in GitHub Actions

In this activity, we'll set up Minikube as a continuous integration (CI) step in GitHub Actions to deploy a Node.js app to Kubernetes.

### Tasks:

1. **Create Dockerfile for Node.js App**
2. **Create package.json file**
3. **Create Server.js file**
4. **Create Kubernetes Deployment and Service file**
5. **Set up GitHub Actions Workflow to Deploy to Minikube using GitHub Actions**

### Video Explanation:
[Watch the video explanation here](LINK_OF_ACTIVITY2_VIDEO_EXPLANATION)

### GitHub Repository:
[Access the GitHub repository here](LINK_OF_ACTIVITY2_GITHUB_REPO)

---

## Activity 3: Implementing CI/CD Pipeline with GitHub Actions and GitHub Pages in a React App

In this activity, we will set up a CI/CD pipeline using GitHub Actions and deploy a React app to GitHub Pages.

### Steps:

1. Create a basic React application using Vite.


2. Create a GitHub repository for our project.

3. Set up CI/CD workflow with GitHub Actions in our project directory. See the workflow file below.

### GitHub Repository:
[Access the GitHub repository here](LINK_OF_ACTIVITY3_GITHUB_REPO)

### Video Explanation:
[Watch the video explanation here](LINK_OF_ACTIVITY3_VIDEO_EXPLANATION)

```yaml
name: DevOps-GitHubActions

on: push

jobs:
# Build Job
build:
 runs-on: ubuntu-latest
 steps:
   - name: Checkout Code
     uses: actions/checkout@v3
   - name: Install Node
     uses: actions/setup-node@v3
     with:
       node-version: 18.x
   - name: Install Dependencies
     run: npm install
   - name: Build Project
     run: npm run build
   - name: Upload artifact to enable deployment
     uses: actions/upload-artifact@v3
     with:
       name: production-files
       path: ./dist

# Deploy Job
deploy:
 # Add a dependency to the build job
 needs: build
 # Specify runner + deployment step
 runs-on: ubuntu-latest
 steps:
   - name: Download artifact
     uses: actions/download-artifact@v3
     with:
       name: production-files
       path: ./dist
   - name: Deploy to GitHub Pages
     uses: peaceiris/actions-gh-pages@v3
     with:
       github_token: ${{ secrets.TOKEN }}
       publish_dir: ./dist
