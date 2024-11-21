# aws-deploy

## build docker image and push to dockerhub
- to build docker image for linux distribution
  - docker buildx build --platform linux/amd64 -t dockerhub_namespace/image_name:tag_name .
- to push the image to dockerhub
  - docker push dockerhub_namespace/image_name:tag_name

## deploy to aws
- create aws account
- login to aws account
- select the Region (closest to your geographical area)
- create a VPC (virtual private cloud) or use the default VPC
- create a Security Group (firewall)
- add ingress/inbound rules and egress/outbound rules to the Security Group
- create a Key Pair for remote login through ssh
- create a EC2 instance
  - by using AMI (Amazon Machine Image/ software image) that is free tier eligible
  - by using Instance Type (virtual server type) that is free tier eligible
  - by selecting the already created Key Pair for login
  - by selecting the already created Security Group
- launch the above created EC2 instance and wait till instance state becomes running
- copy the public IP address of the running EC2 instance
- in order to connect to EC2 instance from local machine through ssh connection
  - open the terminal from the location of .pem file was saved
  - run the command
    - ssh -i key_file_name.pem ec2-user@public_ip_of_the_ec2_instance
  - after connected to EC2 instance (after ssh connection established to ec2 instance)
    run below commands inside the ec2 instance
    - sudo yum update -y
    - sudo yum install -y docker
    - sudo service docker start
    - sudo docker run -d -p 80:8080 dockerhub_namespace/image_name:tag_name
      
## in the browser
- http:ec2_instance_public_ip:8080
- http:ec2_instance_public_ip:8080/api/v1/demo
