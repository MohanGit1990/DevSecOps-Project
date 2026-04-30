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

13. Install kubectl in central server
      sudo snap install kubectl --classic

14. Create/configure kubeconfig file with the cluster name
      aws eks update-kubeconfig --region us-west-2 --name devops-cluster

      
    

      

   
    
