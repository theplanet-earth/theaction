# 🚀 theaction

> Centralized GitHub Actions for building and publishing Docker images across the **theplanet**.

## 📦 Purpose

This repository collects and centralizes a set of reusable GitHub Actions, primarily focused on:

- 🐳 **Building and publishing Docker images**
- ☕ **Building Maven-based Spring Boot projects**

These actions are designed to be **triggered automatically** by other repositories (e.g., `thedashboard`, `thehumongous`, etc.) whenever a pull request is merged into either:

- `master` ➜ Builds and pushes Docker images to **DockerHub** with proper version tags  
- `staging` ➜ Builds and pushes Docker images to **GitHub Container Registry (GHCR)** using the `latest` tag

This structure promotes **reusability**, **consistency**, and **automation** across projects in the [@theplanet-earth](https://github.com/theplanet-earth) organization.

## ⚙️ Setup: Enabling These Actions in Other Projects

To trigger the GitHub Actions in `theaction` from other repositories, you need to:

### 1. 🔐 Define the `GH_PAT` Secret (per repository)

In each triggering repository, create a repository secret named `GH_PAT`. 📘 [How to create a repository secret](https://docs.github.com/en/actions/how-tos/writing-workflows/choosing-what-your-workflow-does/using-secrets-in-github-actions#creating-secrets-for-a-repository)

Use the value of the **Personal Access Token** (PAT) called `trigger-autobuild`.  

- 🕓 Validity: Max 30 days  
- 🔒 Token type: **Fine-grained personal access token**
- 🔧 Permissions:
  - Access: `@theplanet-earth`
  - Repository access: `theplanet-earth/theaction`
  - Repository permissions:
    - ✅ Read access to metadata  
    - ✅ Read and Write access to actions  

This token must be generated under the **Developer Settings** of the account `andreagalle`.

➡️ Set or update this secret in the following repositories:

1. [`thedashboard`](https://github.com/theplanet-earth/thedashboard)
2. [`thehumongous`](https://github.com/theplanet-earth/thehumongous)
3. [`theburden`](https://github.com/theplanet-earth/theburden)
4. [`theshort`](https://github.com/theplanet-earth/theshort)
5. [`theblend`](https://github.com/theplanet-earth/theblend)

---

### 2. 🔐 Define Organization-Level Secrets for `theaction`

Because `theaction` is a **public repo**, you can use organization-level secrets to allow its workflows to push images.  

Create the following secrets. 📘 [How to create organization-level secrets](https://docs.github.com/en/actions/how-tos/writing-workflows/choosing-what-your-workflow-does/using-secrets-in-github-actions#creating-secrets-for-an-organization)

#### ✅ `GH_PAT` (for GitHub code access)

Use the value of the fine-grained PAT called `docker-autobuild`.

- 🕓 Validity: Max 30 days  
- 🔒 Token type: **Fine-grained personal access token**
- 🔧 Permissions:
  - Access: `@theplanet-earth`
  - Repository access:
    - `theplanet-earth/theosm`
    - `theplanet-earth/thedashboard`
    - `theplanet-earth/thehumongous`
    - `theplanet-earth/theburden`
    - `theplanet-earth/theshort`
  - Repository permissions:
    - ✅ Read access to metadata  
    - ✅ Read and Write access to code  

#### 🐙 `GHCR_TOKEN` (for GitHub Container Registry access)

Use the value of the (**classic**) PAT called `container-registry`.

- 🕓 Validity: Max 30 days  
- 🔒 Token type: **Personal access tokens (classic)**
- 🔧 Scopes:
  - `write:packages` → Upload to GHCR  
  - `read:packages` → Download from GHCR  
  - `delete:packages` → Delete from GHCR  

Again, this tokens must be generated under the **Developer Settings** of the account `andreagalle`.

Make these secrets **available only to** the repository `theplanet-earth/theaction`.

## 🐋 Docker Image Publishing

### 🛠️ DockerHub

> 🔄 In progress: We're transitioning from GHCR to **DockerHub** for image publication.  
Stay tuned in [#5](https://github.com/theplanet-earth/theaction/issues/5) for tracking this migration.

### 🔐 Authentication

For more informations on the authentication mechanism, refer to the following link:

📘 [Authenticating with a personal access token (classic)](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-container-registry#authenticating-with-a-personal-access-token-classic)

### 🏷️ Labelling Best Practices

To better understand how to label Docker images, before pushing them, refer to this:

📘 [Labelling container images](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-container-registry#labelling-container-images)

## 🧩 Contributing

Feel free to open issues or propose improvements — this repo is open to collaboration and contributions to enhance CI/CD flows across the entire **theplanet** ecosystem.
