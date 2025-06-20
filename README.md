README.md



# 🐳 CI/CD Node.js Web App with Docker & Render

This project demonstrates how to build a simple Node.js application, containerize it with Docker, and deploy it automatically using GitHub and Render's CI/CD.

---

## 📁 Project Structure

ci-cd-docker-webapp/ ├── app.js ├── Dockerfile ├── package.json ├── .dockerignore └── render.yaml
---

## 🧰 Prerequisites

- Node.js (v18+)
- npm
- Docker installed and running
- Git + GitHub account
- Render account [https://render.com](https://render.com)

---

## 🚀 Step-by-Step Guide

### 1. Create the Project Directory

```bash
mkdir ci-cd-docker-webapp && cd ci-cd-docker-webapp
npm init -y

2. Install Express
npm install express

3. Create the App File
Create a file called app.js and paste the following:
const express = require('express');
const app = express();
const port = process.env.PORT || 3000;

app.get('/', (req, res) => res.send('Hello from Render CI/CD!'));

app.listen(port, () => console.log(`App running on port ${port}`));

4. Create a .dockerignore File
This avoids copying unnecessary files into your image.
touch .dockerignore
Content:
node_modules
npm-debug.log

5. Create a Dockerfile
# Use official Node image
FROM node:18-alpine

# Set working directory
WORKDIR /app

# Copy files and install dependencies
COPY package*.json ./
RUN npm install

# Copy the rest of the app
COPY . .

# Expose the port the app runs on
EXPOSE 3000

# Start the app
CMD ["node", "app.js"]

6. Build the Docker Image (Optional for Local Test)
docker build -t ci-cd-docker-webapp .
docker run -p 3000:3000 ci-cd-docker-webapp
Visit http://localhost:3000 to confirm it works.

7. Initialize Git & Push to GitHub
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/YOUR_USERNAME/ci-cd-docker-webapp.git
git branch -M main
git push -u origin main
Replace the GitHub URL with your actual repository.

8. Create render.yaml for Auto Deploy
Render uses this file to configure deployment.
services:
  - type: web
    name: ci-cd-node-app
    runtime: docker
    repo: https://github.com/YOUR_USERNAME/ci-cd-docker-webapp
    branch: main
    plan: free
    autoDeploy: true
Replace the repo URL with your GitHub repo.

9. Deploy to Render
1. Visit https://render.com
2. Click "New Web Service"
3. Choose "Deploy from GitHub Repo"
4. Authorize access and select your repository
5. Render detects the Dockerfile and deploys the app

10. 🎉 Done!
Render provides a live URL like:
https://ci-cd-node-app.onrender.com
Visit it to confirm your app is live and deployed using CI/CD!

📌 Notes
* You can edit your app and push updates. Render will auto-deploy.
* Make sure Docker is running if testing locally.
* If you want to extend this with GitHub Actions, let me know!

✍️ Author
Gerald Ikenwaike — DevOps Engineer | Web Developer | Pianist | Music Producer 🌐 GitHub: github.com/Gerald-Ikenwaike | LinkedIn: www.linkedin.com/in/arinze-ikenwaike-425620183


