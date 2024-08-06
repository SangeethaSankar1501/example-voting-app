# example infrastructure set-up and application deployment model (CD) 

For the development environment, I have used AWS Codepipeline and Codebuild to build, tag and push the images to docker hub. i have installed K8s cluster in AWS EC2. I am using Githubactions to deploy the k8s manifest files to the K8s. CodePipeline orchestrates the build stage and automatically triggering builds whenever changes are pushed to GitHub repository.  After CodeBuild has successfully built and pushed the images to Docker Hub, GitHub Actions takes over to handle the deployment. I  have set up workflow that apply Kubernetes manifests in git repo to Kubernetes cluster running on AWS EC2.

![image](https://github.com/user-attachments/assets/6597c74c-a4b4-43ea-83d0-34faafbe99e3)

I have provided necessary access to the services using IAM roles. I have stored docker credentials in SSM Parameter store and provided the codebuild role with SSM access.

To mimic the production environment, we can deploy application in 2 availability zone by using an autoscaling group and load balancer for traffic. Deploying the application in private subnet and the requests come through load balancer. The application can connect to internet using NAT gateway. 
![alt text](image-1.png)
