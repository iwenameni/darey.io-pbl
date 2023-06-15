### PROJECT 11: Ansible – Automate Project 7 to 10

STEP 1: INSTALL AND CONFIGURE ANSIBLE ON EC2 INSTANCE

Update Name tag on your Jenkins EC2 Instance to Jenkins-Ansible. We will use this server to run playbooks.

In your GitHub account create a new repository and name it ansible-config-mgt.

Instal Ansible;

sudo apt update

sudo apt install ansible

Check your Ansible version by running;

ansible --version

We configure Jenkins build job to save the repository content every time we change it.
Create a new Freestyle project ansible in Jenkins and point it to your ‘ansible-config-mgt’ repository.
Configure Webhook in GitHub and set webhook to trigger ansible build.
Configure a Post-build job to save all (**) files.
Test the setup by making some change in README.MD file in master branch and make sure that builds starts automatically and Jenkins saves the files (build artifacts) in following folder

ls /var/lib/jenkins/jobs/ansible/builds/<build_number>/archive/

Allocate an Elastic IP to your Jenkins-Ansible server to prevent reconfiguring our GitHub webhook to a new IP addres whenever we stop and start our server.

