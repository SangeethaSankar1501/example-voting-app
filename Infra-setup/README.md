# example infrastructure set-up and application deployment model (CD) 

For the development environment, I have used AWS Codepipeline and Codebuild to build, tag and push the images to docker hub. i have installed K8s cluster in AWS EC2. I am using Githubactions to deploy the k8s manifest files to the K8s. CodePipeline orchestrates the build stage and automatically triggering builds whenever changes are pushed to GitHub repository.  After CodeBuild has successfully built and pushed the images to Docker Hub, GitHub Actions takes over to handle the deployment. I  have set up workflow that apply Kubernetes manifests in git repo to minikube running on AWS EC2.

I have provided necessary access to the services using IAM roles. I have stored docker credentials in SSM Parameter store and provided the codebuild role with SSM access.

![image](https://github.com/user-attachments/assets/3cbc89c9-a4c8-4098-bc33-811990b7426c)

![image](https://github.com/user-attachments/assets/ac4320bb-f7fa-407f-a111-ef53401462f4)

I have attempted to set up the Minikube on EC2, but faced some technical issues that prevented me from completing the deployment.

![image](https://github.com/user-attachments/assets/06946e99-bfa8-47b9-a856-48ed6c38dd19)

I used bastian server in public subnet to connect to the EC2 in private subnet to install minikube with docker driver. I attempted to create docker webhook to trigger the github workflow once the image is pushed to dockerhub. i have updated imagepullsecrets in the k8s yaml files to pull the images from my docker repository and deploy the files to the kubernetes.

---------------------------------------------------------------------------------------------------------------------------------------------------------
To mimic the production environment, we can deploy application in 2 availability zone by using an autoscaling group and load balancer for traffic. Deploying the application in private subnet and the requests come through load balancer. The application can connect to internet using NAT gateway.

![image](https://github.com/user-attachments/assets/8de0941d-7563-46b8-bbfe-a126c1da47d4)


![image](https://github.com/user-attachments/assets/ba59ce37-160e-475f-b201-3b1bdd557b01)


-----------------------------------------------------------------------------------------------------------------------------------------
I encountered some challenges while trying to apply a k8s yaml files to Minikube. Despite my best efforts, I was unable to successfully run the kubectl apply command, as the Kubernetes configuration files were not being recognized by the kubectl command.

I performed few troubleshooting steps to resolve the issue:
*Checked the Kubernetes configuration context to ensure that the Minikube context was being used.
*Verified the permissions on the Kubernetes configuration files and the resource specification file.
*Attempted to recreate the Minikube cluster to see if that would resolve the issue.
