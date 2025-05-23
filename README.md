# 🚀 Counter App – CI/CD with Netlify & GitHub Actions

## **📌 Overview**
This project uses **Netlify** for hosting and **GitHub Actions** for continuous deployment. Every change pushed to the `main` branch is automatically built and deployed to Netlify.

---

## **🚀 Setup & Deployment Steps**
### **1️⃣ GitHub Repository**
- Create a repo (`counter-app`) on GitHub.
- Clone the repo:
  ```bash
  git clone https://github.com/YOUR-USERNAME/counter-app.git
  cd counter-app

Create a React App
Install and set up React:
npx create-react-app .
npm start

Push the initial code to GitHub:

bash
git add .
git commit -m "Initial commit"
git push origin main

3️⃣ Deploy to Netlify
Connect the repo to Netlify (GitHub → New Project → Select Repo).

Set deployment settings:

Build Command: npm run build

Publish Directory: build

Click Deploy 🎉

4️⃣ CI/CD – GitHub Actions Workflow
📌 Create GitHub Actions Workflow
Create .github/workflows/netlify.yml in your project.

Add the following configuration:
name: Deploy to Netlify

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Repository
        uses: actions/checkout@v3

      - name: Set up Node.js
        uses: actions/setup-node@v3
        with:
          node-version: 18

      - name: Install Dependencies
        run: npm install

      - name: Build Project
        run: npm run build

  deploy:
    needs: build
    runs-on: ubuntu-latest
    steps:
      - name: Deploy to Netlify
        uses: nwtgck/actions-netlify@v2
        with:
          publish-dir: ./build
          production-branch: main
          deploy-message: "Netlify deployment from GitHub Actions"
          netlify-auth-token: ${{ secrets.NETLIFY_AUTH_TOKEN }}
          netlify-site-id: ${{ secrets.NETLIFY_SITE_ID }}
5️⃣ Add Netlify Secrets in GitHub
Go to GitHub → Your Repo → Settings → Secrets & Variables → Actions.

Click "New Repository Secret", then add:

Name: NETLIFY_AUTH_TOKEN → Value: Your Netlify API Token.

Name: NETLIFY_SITE_ID → Value: Your Netlify Site ID.
6️⃣ Push & Test CI/CD
Add and commit GitHub Actions workflow:

git add .github/workflows/netlify.yml
git commit -m "Added GitHub Actions for Netlify deployment"
git push origin main
To manually trigger CI/CD:

bash
git commit --allow-empty -m "Trigger CI/CD pipeline"
git push origin main

🎯 Auto-Deploy in Action
Modify any code (App.js).

Push changes:

git add .
git commit -m "Updated UI"
git push origin main
Your app will automatically deploy to Netlify! 🚀🎉