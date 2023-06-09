# 3rd-semester-final-project

This repo contains terraform files neccessary to deploy a jenkins server on aws. It also contains more configuration files that were used to automate the deployment of the sock-shop app and an nginx app on an AWS EKS cluster through a jenkins pipeline


#

![Altschool Africa](https://github.com/tuyojr/cloudTasks/blob/main/logos/AltSchool.svg)

## REQUIREMENTS

1. A control node with git, terraform installed.
2. AWS account, AWS CLI installed and configured.
3. Terraform Installed on your local system.

## SETTING UP THE JENKINS SERVER

In the `deploy-jenkins-with-terraform` folder above, you will find the terraform code to set up the Jenkins server on ubuntu 20.04. Run the following commands to set up the server.

```bash
terraform init
terraform apply --auto-approve
```

This will create the VPC (and all its other components), I'm using a pre-existing keypair with it. You can change the keypair name in the `jenkins-server.tf` file. There's also a script to install all the required packages on the server. You can find it in the `jenkins-server-script.sh`. When the infrastructure is complete, the public IP address of the server will be displayed. You can use this to access the server. `http://<public-ip-address>:8080`.
SSH into the server and display the required password to unlock Jenkins. You can use this to login to the server.
Configure your github and aws credentials, create a pipeline, and you are good to go.

## SETTING UP THE EKS CLUSTER AND DEPLOYING THE APPLICATIONS

In the `jenkins-pipeline-to-deploy-to-eks/terraform` folder, there are configurations files to provision the eks cluster.
In the `jenkins-pipeline-to-deploy-to-eks/kubernetes` folder, there are configuration files to deploy the applications on the cluster and create a DNS on route53.

## MONITORING THE APPLICATIONS WITH PROMETHEUS

There are configuration files to deploy prometheus and grafana in the `jenkins-pipeline-to-deploy-to-eks/monitoring` folder. You can use these to monitor the applications. To access the prometheus dashboard, you can use the following command on your jenkins server.

```bash
kubectl port-forward svc/prometheus-server 8081:9090 -n monitoring --address 0.0.0.0
```

To access the grafana dashboard, you can use the following command on your jenkins server.

```bash
kubectl port-forward svc/grafana 8082:80 -n monitoring --address 0.0.0.0 .
```

## DEPLOYED APPS
![nginx](https://github.com/dubem2/CICD-pipeline-to-deploy-apps-to-EKS-cluster/tree/main/images/nginx.png)
![sock-shop](https://github.com/dubem2/CICD-pipeline-to-deploy-apps-to-EKS-cluster/tree/main/images/sock-shop.png)










