This is a task to deploy our web application using Git , Docker and jenkins . Using these tools we can make our task as possible as automate . 
it is something like that whenever developer commit their code then automatically code push to some SCM system like Github
and from there jenkins pulling code and deploying it in a container.
The purpose of this task to automate the of the production team. In simple way this task automatically first clone the developer repository from the GitHub.
Then after cloning it checks weather the code is running fine in developer environment, if yes, then it'll automatically merge the developer branch to the
master/production branch and push to master/production branch. Finally whenever code is pushed to master/production branch it'll automatically clone the
repository and deploy the code at production environment.

Required Tools:-
1.Git
2.Github
3.Jenkins
4.Docker

Pre- requisite -
In which base operating system you are working run these commands-
1. systemctl start docker — for starting docker services so that jenkins can deploy our webserver.
2. systemctl start jenkins — for starting jenkins and we can use jenkins in windows using base OS ip and port 8080 . jenkins run on port no 8080.
3.systemctl stop firewalld — to stop firewall

Task description -
JOB-1
If Developer push to dev branch then Jenkins will fetch from dev and deploy on dev-docker environment.
JOB-2
If Developer push to master branch then Jenkins will fetch from master and deploy on master-docker environment.
both dev-docker and master-docker environment are on different docker containers.
JOB-3
Manually the QA team will check (test) for the website running in dev-docker environment.
If it is running fine then Jenkins will merge the dev branch to master branch and trigger #job2.

Creating jobs -
job 1 -
If Developer push to dev branch then jenkins will fetch from dev and deploy on dev-docker environment
First in SCM select git following which add all the necessary details like(repo url,branch where to clone from)
then the shell code which will clone from dev branch make developer directory in which all the developer's code will be kept and
then launch the dev enviroment using docker.

job 2 -
In this job if developer push code to master branch then jenkins will come to master branch and will pull code and deploy.

job 3-
Manually the QA team will check (test) for the website running in dev-docker environment. If it is running fine then Jenkins will merge the
dev branch to master branch and trigger #job2
In this, I have used status command using curl to check whether the app is running or not if it's running fine it'll merge the developer 
branch to master branch.Then I have added two more things first in SCM section of git I have added the credential 
(username and password of my github account) and the post-build action for pushing the code if the app is running fine.
JOB3 If Developer push to master branch then Jenkins will fetch from master and deploy on master-docker environment.
both dev-docker and master-docker environment are on different docker containers.
If this job will successfully run then it will automatically build job 2 again and 
It'll fetch the code from the master branch and start the production environment.
