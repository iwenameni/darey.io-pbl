### CONTINOUS INTEGRATION PIPELINE FOR TOOLING WEBSITE

## Step 1 – Install Jenkins server

sudo apt update

sudo apt install default-jdk-headless

curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update

sudo apt-get install jenkins

sudo systemctl status jenkins

## Step 2 – Configure Jenkins to retrieve source codes from GitHub using Webhooks

In this part, you will learn how to configure a simple Jenkins job/project (these two terms can be used interchangeably).

This job will will be triggered by GitHub webhooks and will execute a ‘build’ task to retrieve codes from GitHub and store it locally on Jenkins server.

ls /var/lib/jenkins/jobs/tooling_github/builds/<build_number>/archive/

## Step 3 – Configure Jenkins to copy files to NFS server via SSH

sudo chown -R nobody:nobody /mnt

sudo chmod -R 777 /mnt

cat /mnt/apps/README.md


![prj9-1](https://github.com/iwenameni/darey.io-pbl/assets/111616140/dda833ff-e2f9-4643-8cdf-be10ed28b680)

![prj9-2](https://github.com/iwenameni/darey.io-pbl/assets/111616140/a38761f1-b43d-4cbc-991b-42721a4140d3)

![prj9-3](https://github.com/iwenameni/darey.io-pbl/assets/111616140/1c94f44e-3c80-443f-9bb9-c6fc5122f38d)

![prj9-4](https://github.com/iwenameni/darey.io-pbl/assets/111616140/3806ffc1-918e-4cd9-9ba2-359a5e8b5dc0)

![nfs-output1](https://github.com/iwenameni/darey.io-pbl/assets/111616140/c4994324-ad4b-474a-9a4a-0bc163080092)

![nfs-output2](https://github.com/iwenameni/darey.io-pbl/assets/111616140/a3226d36-f0d8-41b1-a6d7-c0ca6957a0e4)

![nfs-output3](https://github.com/iwenameni/darey.io-pbl/assets/111616140/08f9b24d-222b-4b60-b122-b4a8f4de9af3)

![nfsoutput4](https://github.com/iwenameni/darey.io-pbl/assets/111616140/0338876a-4bd2-47d4-9c53-25cab21954d9)

![build-output](https://github.com/iwenameni/darey.io-pbl/assets/111616140/458eef7d-adc9-435b-aa07-0bce8ac71001)

![build-output2](https://github.com/iwenameni/darey.io-pbl/assets/111616140/da005b90-5afd-4a93-970f-1a6e032f70f4)

![builds](https://github.com/iwenameni/darey.io-pbl/assets/111616140/f945d606-f2d8-4e17-a5d5-a19af858412c)
