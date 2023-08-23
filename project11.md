### PROJECT 11: Ansible – Automate Project 7 to 10

## STEP 1: INSTALL AND CONFIGURE ANSIBLE ON EC2 INSTANCE

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

## Step 2 – Prepare your development environment using Visual Studio Code

Install VSC and configure it to connect to your newly created GitHub repository.

We clone down the ansible-config-mgt repo to our Jenkins-Ansible instance

git clone <ansible-config-mgt repo link>

## Step 3: ANSIBLE DEVELOPMENT

In our ansible-config-mgt GitHub repository, we create a new branch that will be used for development of a new feature.

We give our branches descriptive and comprehensive names

Checkout the newly created feature branch to your local machine and start building your code and directory structure

Create a directory and name it playbooks – it will be used to store all your playbook files.

Create a directory and name it inventory – it will be used to keep your hosts organised.

Within the playbooks folder, create your first playbook, and name it common.yml

Within the inventory folder, create an inventory file (.yml) for each environment (Development, Staging Testing and Production) dev, staging, uat, and prod respectively.

## Step 4 – Set up an Ansible Inventory

An Ansible inventory file defines the hosts and groups of hosts upon which commands, modules, and tasks in a playbook operate. Since our intention is to execute Linux commands on remote hosts, and ensure that it is the intended configuration on a particular server that occurs, it is important to have a way to organize our hosts in such an Inventory.

Save below inventory structure in the inventory/dev file to start configuring our development servers, replacing the IP addresses according to our own setup.

Note: Ansible uses TCP port 22 by default, which means it needs to ssh into target servers from Jenkins-Ansible host – for this you can implement the concept of ssh-agent. Now you need to import your key into ssh-agent:

eval `ssh-agent -s`

ssh-add <path-to-private-key>

Confirm the key has been added with the command below, you should see the name of your key

ssh-add -l

Now, ssh into your Jenkins-Ansible server using ssh-agent

ssh -A ubuntu@public-ip

Note: our Load Balancer user is ubuntu and user for RHEL-based servers is ec2-user.

Update your inventory/dev.yml file with this snippet of code:

[nfs]
<NFS-Server-Private-IP-Address> ansible_ssh_user='ec2-user'

[webservers]
<Web-Server1-Private-IP-Address> ansible_ssh_user='ec2-user'
<Web-Server2-Private-IP-Address> ansible_ssh_user='ec2-user'

[db]
<Database-Private-IP-Address> ansible_ssh_user='ec2-user' 

[lb]
<Load-Balancer-Private-IP-Address> ansible_ssh_user='ubuntu'

## Step 5 – Create a Common Playbook

It is time to start giving Ansible the instructions on what you needs to be performed on all servers listed in inventory/dev.

In common.yml playbook you will write configuration for repeatable, re-usable, and multi-machine tasks that is common to systems within the infrastructure.

Update your playbooks/common.yml file with following code:

---
- name: update web, nfs and db servers
  hosts: webservers, nfs, db
  remote_user: ec2-user
  become: yes
  become_user: root
  tasks:
    - name: ensure wireshark is at the latest version
      yum:
        name: wireshark
        state: latest

- name: update LB server
  hosts: lb
  remote_user: ubuntu
  become: yes
  become_user: root
  tasks:
    - name: Update apt repo
      apt: 
        update_cache: yes

    - name: ensure wireshark is at the latest version
      apt:
        name: wireshark
        state: latest

This playbook is divided into two parts, each of them is intended to perform the same task: install wireshark utility (or make sure it is updated to the latest version) on your RHEL 8 and Ubuntu servers. It uses root user to perform this task and respective package manager: yum for RHEL 8 and apt for Ubuntu.

## Step 6 – Update GIT with the latest code

Now all of your directories and files live on your machine and you need to push changes made locally to GitHub.

Commit your code into GitHub:

use git commands to add, commit and push your branch to GitHub.

git status

git add <selected files>

git commit -m "commit message"

Create a Pull request (PR)

Merge the code to the master branch.

Head back on your terminal, checkout from the feature branch into the master, and pull down the latest changes.

Once your code changes appear in master branch – Jenkins will do its job and save all the files (build artifacts) to /var/lib/jenkins/jobs/ansible/builds/<build_number>/archive/ directory on Jenkins-Ansible server.

## Step 7 – Run first Ansible test

Now, we will execute ansible-playbook command and verify if the playbook actually works:

cd ansible-config-mgt

ansible-playbook -i inventory/dev.yml playbooks/common.yml

You can go to each of the servers and check if wireshark has been installed by running which wireshark or wireshark --version

