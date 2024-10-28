# 🐳 Azure DevOps CI/CD Pipeline Project with SonarQube & AKS

This repository contains the **CI/CD pipeline configuration** for the [BoardGame](https://github.com/jaiswaladi246/Boardgame/tree/main) project**. This repository contains the CI/CD pipeline setup for a Maven-based application. While this project was initially developed using both AWS and Azure, the following instructions focus on Azure DevOps. This pipeline uses SonarQube for code quality checks, Docker for containerization, and Azure Kubernetes Service (AKS) for deployment.


## 📂 Technologies Used:

This repository uses the open-source boardgame application, which I have integrated with my Azure DevOps project. 
- Azure DevOps: For CI/CD pipeline creation.
- SonarQube: For code quality analysis.
- Docker: For containerization.
- Azure Kubernetes Service (AKS): For deployment.
- Maven: As the project build tool.


## 🛠️ Prerequisites
To complete this project, ensure you have:

- An **Azure DevOps** account.
- A **GitHub** repository for project version control.
- **SonarQube** running via Docker for code analysis.
- **Azure Kubernetes Service (AKS)** for application deployment.
- **Java (17)**, **Maven**, and **Trivy** installed on the agent VM.


## 🚀 Project Setup

### Step 1: Set Up SonarQube for Code Quality Analysis

1. **Run SonarQube Docker Image:** To check code quality, we’ll use a Docker image of SonarQube with a community branch plugin. Run the following command:
   ```bash
   docker run -d --name sonar -p 9000:9000 mc1arke/sonarqube-with-community-branch-plugin
   ```

2. **Access the SonarQube Interface:** After running the container, you can access SonarQube via:
    - `localhost:9000` (if running locally) or
    - `your_ip_address:9000` (if running on a VM).

### Step 2: Import the GitHub Project into Azure DevOps

1. **Create a New Azure DevOps Project:**
   - Go to your Azure DevOps account, create a new project, and import your GitHub repository.
   - You can also import this GitHub repository:
     ```bash
     https://github.com/khizraghaffarkk/Azure-DevOps-CI-CD-Pipeline-Project-with-SonarQube-and-AKS.git
     ```

2. **Set Up a Classic Pipeline:**
   - In Azure DevOps, choose the **Classic** pipeline (this example uses a Maven-based project).
   - Select the **Maven** template for the pipeline.
   - Choose an **Agent Pool** and specify agent details.


     ```bash
     ssh -i <your-key-file> azureuser@<vm-public-ip>
     ```

### Step 3: Configure a Virtual Machine as a Pipeline Agent
To run the pipeline, you need a VM to act as an agent. Use the following commands to set up the VM as an Azure DevOps agent:

1. **Download and Create the Agent:**
     ```bash
     mkdir myagent && cd myagent
     tar zxvf ~/Downloads/vsts-agent-linux-x64-3.246.0.tar.gz
     ```
2. **Configure the Agent:**
   - Enter your Azure DevOps organization URL:
      `https://dev.azure.com/your_organization_name`
   - Provide your **Personal Access Token (PAT)** from Azure DevOps.

3. **Run the Agent:**
     ```bash
     ./run.sh
     ```
### Step 4: Install Java, Maven, and Trivy

1. **Install Java (17):**
   - Ensure Java 17 is installed as it is required by the Maven project.

2. **Install Maven:**
   - Maven is required to build and manage dependencies for the project.

3. **Install Trivy:**
   - Trivy can be used for vulnerability scanning of Docker images.

### Step 5: Configure and Run the Pipeline

1. **Integrate SonarQube with Azure DevOps:**
   - Install the **SonarQube** Extension from the **Azure Marketplace**.
   - Add the SonarQube extension to your Azure DevOps organization.
   - In your agent job, configure the **SonarQube server URL** and provide an **authentication token** created in the SonarQube interface.
     
2. **Docker Hub Integration:**
   - Link your **Docker Hub** account with Azure DevOps.
   - Specify the **container repository** where the Docker image will be pushed.
   - Provide the path to the Dockerfile in pipeline parameters.

3. **Install Trivy:**
   - Trivy can be used for vulnerability scanning of Docker images.


### 🌀 Deployment with Azure Kubernetes Service (AKS)
#### Step 6: Deploy to AKS
1. **Set Up Azure Kubernetes Service:**
   - Create an AKS cluster to host the application.

2. **Store Artifacts:**
   - In Azure DevOps, **Artifacts** can be used to store build outputs like Maven packages.

3. **Create a CD Pipeline for Deployment:**
   - Set up a **CD pipeline** to automate integration and deployment whenever changes are made to the application.
   - Install `kubectl` on the VM and use it to apply Kubernetes specifications.

4. **Monitor Deployment:**
   - Use `kubectl` to verify deployment
     ```bash
     kubectl apply -f <your-deployment-file>.yaml
     kubectl get pods
     ```
   - Confirm that pods are created and the application is running.

### 📈  Monitoring and Quality Checks
To check the status of your application:
**1. Code Quality in SonarQube:**
   - Access the SonarQube interface to view code quality and coverage reports.
**2. Docker Image Verification:**
   - Check Docker Hub to ensure the image was successfully created and pushed.
**3. Application Status in AKS:**
   - Use Azure Kubernetes Service tools to confirm the application is running as expected.  

### 🤖 Additional Resources
- Azure DevOps Documentation 
- SonarQube Documentation
- Kubernetes Documentation
- Maven Documentation
