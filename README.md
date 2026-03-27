# Docker NGINX Azure Next.js App

This repository provides a complete boilerplate for running a **Next.js** frontend application behind an **NGINX** reverse proxy, all containerized using **Docker** and orchestrated with **Docker Compose**. It's pre-configured and optimized for secure deployment to an Azure Virtual Machine within a custom Virtual Network.

## 🚀 Features

- **Next.js Frontend:** A scalable React framework (using TypeScript).
- **NGINX Reverse Proxy:** Handles incoming requests on port 80 and proxies them to the Next.js container, optimizing performance and static file serving.
- **Dockerized Environment:** Fully containerized architecture using Docker Compose for seamless local development and production parity.
- **Secure Azure Architecture:** Designed to be deployed on an Azure VM protected by Azure Firewall and accessed securely via Azure Bastion.

## 📁 Project Structure

- `frontend/`: Contains the Next.js application, its dependencies, and its specific `Dockerfile`.
- `nginx/`: Contains the NGINX configuration and its specific `Dockerfile`.
- `docker-compose.yml`: Orchestrates the building and running of the `frontend` and `nginx` services.

## 🛠️ Prerequisites (Local Development)

Make sure you have the following installed on your local machine:
- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)

## 🏃‍♂️ Getting Started (Local)

1. **Clone the repository:**
   ```bash
   git clone https://github.com/shiranlakshitha/docker-nginx-azure.git
   cd docker-nginx-azure
   ```

2. **Build and spin up the containers:**
   Use Docker Compose to build the images and start the services in detached mode.
   ```bash
   docker-compose up -d --build
   ```

3. **Access the Application:**
   Open your browser and navigate to [http://localhost](http://localhost). The NGINX server will route your traffic directly to the Next.js application.

4. **Stopping the Services:**
   To stop and remove the running containers, execute:
   ```bash
   docker-compose down
   ```

## ☁️ Deploying to Azure

This project was deployed securely using a custom Azure infrastructure setup. Below is the high-level architecture and deployment process:

### 1. Azure Infrastructure Setup
Create the following resources in your Azure portal:
- **Resource Group:** A logical container for your deployment resources.
- **Virtual Network (VNet):** To provide a secure, isolated network for your application.
- **Virtual Machine (VM):** A Linux (e.g., Ubuntu) VM deployed within the VNet to host the Docker containers.
- **Azure Bastion:** Deployed within the VNet to provide secure and seamless SSH access to the VM directly from the Azure portal, without exposing SSH ports to the public internet.
- **Azure Firewall:** Configured to protect the VNet resources, filter incoming/outgoing traffic, and securely route HTTP/HTTPS traffic to the NGINX reverse proxy.

### 2. Application Deployment
Once the infrastructure is provisioned:

1. **Connect to the VM:** Securely SSH into your Azure VM using **Azure Bastion** via the Azure Portal.
2. **Install Dependencies:** Install Docker and Docker Compose on the VM.
3. **Clone the Repository:**
   ```bash
   git clone https://github.com/shiranlakshitha/docker-nginx-azure.git
   cd docker-nginx-azure
   ```
4. **Run the Application:**
   ```bash
   sudo docker-compose up -d --build
   ```
5. **Configure Routing:** Ensure your Azure Firewall and Network Security Groups (NSGs) are configured to allow HTTP (port 80) traffic through to the VM's internal IP address.

## 📝 License
This project is open-source and available under the [MIT License](LICENSE).
