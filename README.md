Configure eureka client as below-

`eureka.client.service-url:defaultZone: http://admin:admin@localhost:8761/discovery/eureka/`  


# AWS
Install **AWS CLI 2** on the machine that will run the build and deploy commands

$ curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
$ unzip awscliv2.zip
$ sudo ./aws/install


**AWS ECR** 

`$ aws ecr get-login-password --region eu-central-1 | docker login --username AWS --password-stdin 144905023660.dkr.ecr.eu-central-1.amazonaws.com`
<br>
`$ docker tag taheruddin/discovery:latest 144905023660.dkr.ecr.eu-central-1.amazonaws.com/taheruddin/discovery:latest`
<br>
`$ docker push 144905023660.dkr.ecr.eu-central-1.amazonaws.com/taheruddin/discovery:latest`