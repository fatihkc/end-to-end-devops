# End-to-End-DevOps
----
## Purpose of the project

With this project I am trying to create a immutable infrastructure with sample deploying pipeline. I hope that project will you to understand basics and integrations of tools that used for CI/CD pipelines.

For now project only includes technologies like Kubernetes, Ansible, Vagrant and Jenkins but in near future tools like SonarQube will be added and playbook will be similar to best practices with some test cases.

## Technologies

- Ansible
- Vagrant 
- Jenkins
 - Configuration As Code
 - Pipeline
- Kubernetes
 - Flannel
- Docker
- Golang


## What happens after startup

After provisioning servers, Ansible uses common role for updating packages, changing DNS settings, disabling swap etc.

Jenkins role is installing Jenkins with some plugins and add admin user. Then uses Configuration As Code plugin to create jobs and credentials.

Docker and Kubernetes roles are basically install required packages and start Kubernetes Cluster with Flannel. 

After triggering job with commiting GitHub repository, app inside src directory is running and testing it. After test pass, Dockerfile is creates and image and push it to the private repository inside DockerHub. Then publish app inside Kubernetes cluster with the help of Ansible playbooks.

----
## Requirements 
- Virtualbox
- Vagrant
- Ansible
- Github account
- Dockerhub account

----
## Usage
### Fork repository

I am using private repository for this project. For testing everything I recommend to use private repository.

Also creating private Dockerhub repository is recommended.

### Change group_vars/all file

Change variables. Don't forget github and dockerhub.

    github_repo: end-to-end-devops
    github_username: ######
    github_password: ######

    dockerhub_repo: end-to-end-devops
    dockerhub_username: #####
    dockerhub_password: #####
    dockerhub_email: #####

### Provisioning

    cd ~
    vagrant up

### Show time

Use ansible-playbook for installing Jenkins, Docker and Kubernetes.

    ansible-playbook -i hosts scratch.yml

### Testing pipeline

Just commit to your project and Jenkins job will be triggered. After finishing job check your application.

    curl 192.168.7.2:32000

## TODO

- SonarQube for Jenkins pipeline
- Molecule for testing playbook
- Write Turkish blog post about project
- Add comments for every step of the project
