# Node.js Application with GitHub Actions Deployment

This repository demonstrates a complete CI/CD pipeline for a Node.js application deploying to an AWS EC2 instance using GitHub Actions and Docker.

## 🚀 Features
- **Node.js Express Server**: A simple API server.
- **Dockerized**: Includes a `Dockerfile` and `docker-compose.yml` for easy containerization.
- **GitHub Actions**: Automated deployment to EC2 on every push to the `main` branch.

## 🛠 Prerequisites
Before you begin, ensure you have:
- An **AWS EC2 instance** (Ubuntu recommended) with:
  - Docker and Docker Compose installed.
  - Port `8080` opened in the Security Group.
- A **GitHub Repository** with the following secrets configured:
  - `SSH_HOST`: Your EC2 Public IPv4 address.
  - `SSH_KEY`: Your private key (`.pem` file content).
  - `SSH_USERNAME`: `ubuntu` (default for AWS Ubuntu instances).

## 📂 Project Structure
- `index.js`: The main application entry point.
- `Dockerfile`: Instructions to build the Docker image.
- `docker-compose.yml`: Orchestrates the application container.
- `.github/workflows/deploy.yml`: The GitHub Actions CI/CD pipeline.

## 📖 How to Use

### 1. Local Development
To run the application locally:
```bash
npm install
npm start
```
Access the app at `http://localhost:8080`.

### 2. Using Docker
To run using Docker Compose:
```bash
docker compose up -d --build
```

### 3. Automated Deployment
1. **Initial Setup on EC2**:
   Connect to your EC2 instance and clone the repository:
   ```bash
   cd /home/ubuntu
   git clone https://github.com/YOUR_USERNAME/GitHub_Actions_Demo.git
   ```

2. **Configure GitHub Secrets**:
   Go to your repository on GitHub: **Settings > Secrets and variables > Actions** and add `SSH_HOST`, `SSH_KEY`, and `SSH_USERNAME`.

3. **Deploy**:
   Simply push your changes to the `main` branch. GitHub Actions will:
   - Connect to your EC2 via SSH.
   - Reset any local changes on the server.
   - Pull the latest code.
   - Rebuild and restart the Docker container.

## 🛑 Common Troubleshooting
- **Permission Denied**: If you see Docker permission errors, the workflow uses `sudo` by default. Ensure the user has sudo privileges.
- **Merge Conflicts**: The workflow runs `git reset --hard origin/main` to ensure the server stays in sync with GitHub, discarding any manual changes on the EC2 instance.
- **Port Access**: If you cannot reach the app, verify that port `8080` is open in your AWS EC2 Security Group.

## 📄 License
ISC
