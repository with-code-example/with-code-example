---
title: How to Analyze Golang Project by Sonarqube With Github Actions/Workflow?
subtitle: Analyze Golang Project by Sonarqube With Github Actions
description: Learn how to use github workflow to check your golang code with sonqrqube.
featured_image: https://res.cloudinary.com/harendra21/image/upload/w_1200/awesome-blog/awesome-golang/How_To_Use_Soanrqube_With_Github_Actions_m37akq.png
thumbnail: https://res.cloudinary.com/harendra21/image/upload/w_400/awesome-blog/awesome-golang/How_To_Use_Soanrqube_With_Github_Actions_m37akq.png
tags: [golang, sonarqube]
comments: true
slug: github-action-for-golang-with-sonarqube
date: 2023-08-06
draft: false
toc: true
series: ['Golang Sonarqube']
---

To analyze a Golang project using GitHub Actions with SonarQube, you'll need to set up a workflow in your repository that triggers the SonarQube analysis on every code push. Here's a step-by-step guide to help you achieve this:

## Setps to analyze golang with sonarqube

### Step 1: Set up SonarQube Server

Ensure you have a running SonarQube server with the SonarGo plugin installed. Refer to the previous answers for instructions on installing SonarQube and the SonarGo plugin.

### Step 2: Obtain SonarQube Token

Generate a SonarQube token that will be used by GitHub Actions to authenticate with the SonarQube server. To create a token, go to your SonarQube server:

1. Log in as an administrator.

2. Navigate to "Administration" > "Security" > "Users."

3. Click on your user account and select the "Tokens" tab.

4. Generate a new token, providing it with a name (e.g., "GitHub Actions").

5. Copy the generated token; you'll need it later.

### Step 3: Configure GitHub Repository Secrets

In your GitHub repository, navigate to "Settings" > "Secrets" and add the following repository secrets:

- `SONAR_TOKEN`: Set this to the SonarQube token you obtained in Step 2.

### Step 4: Create a GitHub Actions Workflow

In your Golang project repository, create a `.github/workflows` directory if it doesn't already exist. Inside this directory, create a new YAML file (e.g., `sonarqube.yml`) for the GitHub Actions workflow.

Add the following content to the `sonarqube.yml` file:

```yaml
name: SonarQube Analysis

on:
  push:
    branches:
      - main  # Change this to the branch you want to analyze

jobs:
  sonarqube:
    name: SonarQube Scan
    runs-on: ubuntu-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v2

    - name: Set up Go
      uses: actions/setup-go@v2
      with:
        go-version: 1.x  # Change this to your desired Go version

    - name: Build Go project
      run: go build

    - name: Run SonarQube Scanner
      uses: sonarsource/sonarqube-scan-action@v1
      with:
        projectBaseDir: ./  # Set this to the project's base directory
        sonarToken: ${{ secrets.SONAR_TOKEN }}
```

Replace `main` with the branch you want to analyze if it's different from the main branch.

### Step 5: Commit and Push

Commit the `sonarqube.yml` file to your repository and push it to trigger the GitHub Actions workflow.

GitHub Actions will now execute the workflow every time there's a push to the specified branch. It will build the Golang project, perform the SonarQube analysis using the SonarGo plugin, and send the results to the SonarQube server.

You can check the analysis results on your SonarQube server by navigating to the project and exploring the code quality metrics, issues, and other findings.

**Please note that you need to adjust the workflow and Golang build steps according to your project's specific requirements, directory structure, and other configurations.**
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTgyMzU3MDM1Ml19
-->