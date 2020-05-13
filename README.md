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

### Part 1 - Create a container image that has Jenkins launched using Dockerfile

!Dockerfile contents(https://github.com/akshayavb99/git-jenkins/blob/master/dockerfile_content.jpg?raw=true)
