# DevSecOps-Project
DevSecOps with ssl certification


1. Create a Central server - to run terraform, EKS cluster
   -t2.medium
2. Update package in EC2
       cmd:  sudo apt update
3. Install AWS CLI

4. Create Access key in AWS user

5. Configure AWS in EC2
       cmd: aws configure
   
6. Install Terraform
       cmd: sudo snap install terraform --classic

7. Terraform files git hub path - https://github.com/jaiswaladi246/FullStack-Blogging-App.git
   Clone the above repo
   update AWS region and availability zones in main.tf file
   update keypair in variables.tf file

8. Run Terraform cmds
   Terraform init
   Terraform plan
   Terraform apply --auto-approve

9. Launch 3 EC2 instances - Jenkins, SonarQube, Nexus

10. Install SonarQube in its server
      Update package - sudo apt update
      Install docker
      cmd: sudo apt install docker.io -y

      Add ubuntu user to docker group
      cmd: sudo usermod -aG docker ubuntu

      Install SonarQube as container
      cmd: docker run -d --name sonardevops -p 9000:9000 sonarqube:lts-community
      

      
  
11. Install Nexus in its server
      Update package - sudo apt update
      Install docker
      cmd: sudo apt install docker.io -y
  
      Add ubuntu user to docker group
      cmd: sudo usermod -aG docker ubuntu
  
      Install Nexus as container
      cmd: docker run -d --name Nexus3 -p 8081:8081 sonatype/nexus3

      Login to container for password
      cmd: docker exec -it <containerid> /bin/bash
      cd sonatype-work/nexus
      cat admin.password
      
12. Install Jenkins in its server
      prerequisite: java
      cmd: sudo apt install openjdk-17-jre-headless

      Install jenkins for ubuntu
      sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc \
        https://pkg.jenkins.io/debian-stable/jenkins.io-2026.key
      echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc]" \
        https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
        /etc/apt/sources.list.d/jenkins.list > /dev/null
      sudo apt update
      sudo apt install jenkins

      Install plugins inside Jenkins
         - sonarqube scanner
         - configfile provider
         - Maven Integration
         - Pipeline Maven Integration
         - k8s plugins
         - docker, docker pipeline

      Configure the tools in Jenkins
          - SonarQube Scanner
             Name: SonarQube Scanner
             version: latest

         - Maven
             Name: maven3
             version: latest

          - Docker
             Name: docker
             Install automatically -> Download from docker.com
             version: latest
      Install latest docker in Jenkins ec2

      Install Trivy in Jenkins ec2
      cmd:
      sudo apt-get install wget gnupg
      wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | gpg --dearmor | sudo tee /usr/share/keyrings/trivy.gpg > /dev/null
      echo "deb [signed-by=/usr/share/keyrings/trivy.gpg] https://aquasecurity.github.io/trivy-repo/deb generic main" | sudo tee -a             /etc/apt/sources.list.d/trivy.list
      sudo apt-get update
      sudo apt-get install trivy
    
14. Install kubectl in central server
      sudo snap install kubectl --classic

15. Create/configure kubeconfig file with the cluster name
      aws eks update-kubeconfig --region us-west-2 --name devops-cluster


16. Create Jenkins pipeline

      For SonarQube: Manage Jenkins -> System -> SonarQube Servers -> Add SonarQube
          Name: sonar
          Server URL: <sonar server url>
          Server Authentication token: <Add the sonar token as secret text> 
      
17. Create RBAC to build the jenkins pipeline in central server where cluster is created

      create a service account, role, role binding in namespace
    

      

   
    
