# Repository for Task 2 of DevOps Assembly Line 
____________________________________________________

## Main Objectives of Task
1.	Create a container image that has Jenkins installed using Dockerfile
2.	When the container is launched, Jenkins must also launch automatically.
3.	Create a job chain of job1, job2, job3, and job4 using the build pipeline in plugins.
4.	Job 1: Pull the GitHub repo automatically when the developers push the repo to GitHub
5.	Job 2: From the files pulled from the GitHub repo, Jenkins should automatically launch a container for the respective programming language (For example, if the code is in PHP, then Jenkins must start the container with PHP already installed).
6.	Job 3: Test if the code in the file is working or not.
7.	Job 4: If the code does not work, send an email to the developer with error messages.
8.	Job 5: If the container where the code is running fails for some reason, then it must start the container again.

## Solution
Partial solution has been developed.

#### Part 1 - Create a container image that has Jenkins installed using Dockerfile

![](https://github.com/akshayavb99/git-jenkins/blob/master/dockerfile_content.jpg?raw=true)

The commands used are for the following purpose:
1. `FROM centos` - It references the base OS for the new image.
2. `RUN yum install wget -y` - Installation of wget command (Used to install Jenkins)
3. `RUN yum install net-tools -y` - Installation of net-tools which form the base of Linux OS networking 
4. `RUN wget -0 /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo` 
5. `RUN rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key` - Commands 4. and 5. are meant for the installation of Jenkins. \(Refer to the link https://www.jenkins.io/download/ \)
6. `RUN yum install java -y && yum install jenkins -y` - Installation of Jenkins and Java as Jenkins is dependant on Java for its working.
7. `RUN yum install git -y` - Installation of Git to perform commands by interacting with GitHub repositories
8. `RUN yum install gedit -y` - Installation of text editor Gedit for performing minor changes in the configuration files of Jenkins to enable email services.
9. `RUN echo -e "jenkins ALL=(ALL) NOPASSWD:ALL" /etc/sudoers` - This allows Jenkins to have maximum access to perform commands by modifying the sudoers file.

After saving the Dockerfile, we use `docker build` to save the container image.

`docker build -t jenkins-os:v2` 

#### Part 2 - Create a container image that has Jenkins installed using Dockerfile
To launch the container we use the `docker run` command.<br> 
`docker run -dit --name jenkinsnew -p 8081:8080 jenkins-os:v2`<br> The command uses different options. `-dit` makes the container run in the background, while providing a terminal. It is also interactive. The container is also exposed to the outside Internet by the use of PATing \( `-p` \) , through the port number 8080. The name of the container is also set using the `--name` option as `jenkinsnew`.

When the container is launched, Jenkins is automatically started, and the initialAdminPassword can also be accessed through the filepath mentioned on the start page of the Web UI Jenkins. To launch the Web UI of Jenkins, type in the web browser **\< Base Os IP:Port Number \>**. This will allow us to login into the Jenkins account.

#### Part 4 - If the code does not work, then send an email to the developer

Sending emails can be done in two ways one of which is enabled by the installation of some plugins. The steps to install the plugins are:
1. Go to Manage Jenkins<br> ![](https://github.com/akshayavb99/git-jenkins/blob/master/email_install1.jpg?raw=true)<br>
2. Select Configure Plugins<br> ![](https://github.com/akshayavb99/git-jenkins/blob/master/email_install2.jpg?raw=true)<br>
3. Select Available. 
4. Select **Email Extension Plugin** and **Email Template Extension Plugin**<br> ![](https://github.com/akshayavb99/git-jenkins/blob/master/email_install3.jpg?raw=true)<br>

Other than plugins, we can also use the default email notifier. For using this option, the steps are as follows:
1. Go to Manage Jenkins<br> ![](https://github.com/akshayavb99/git-jenkins/blob/master/email_install1.jpg?raw=true)<br>
2. Select Configure System <br> ![](https://github.com/akshayavb99/git-jenkins/blob/master/email_install4.jpg?raw=true)<br>
3. Go to the Default Email section and fill in the details as shown below. <br> ![](https://github.com/akshayavb99/git-jenkins/blob/master/email_install5.jpg?raw=true)<br>
