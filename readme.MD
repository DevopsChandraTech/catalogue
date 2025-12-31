catalogue:
----------
1.create git repo for catalogue and get url
2.create ROBOSHOP folder in jenkins and inside the folder create catalogue pipeline for our roboshop project
3.add pipeline for git scm and add url of git without creds and branch is main then apply,save.
4.install node js in AGENT machine why catalogue running on nodejs and java application
5.plug in means inside the javascript code, jenkins use plugins
6.we add Pipeline Utility Steps plugin into jenkins, inside the plugin function called readJSON is on of the function in this function read the values of inside the content of package.json file 
7.install dependencies for npm install to a separate state
8.install docker in AGENT machine to build the image after install must add
    sudo usermod -aG docker ec2-user -> while running the docker in ec2-user
    and restart the docker using systemctl
9.we install the plugin pipeline stageview -> for pipeline apperance.
10.dnf install -y openssl\* openssh\* -> need to install these services and restart the sshd service -> these packages install for latest version of ssl and ssh 
if these missmatch we get a error in ssh failure when we trigged pipeline in jenkins.
after docker installation need install these packages mandatory.
11.with aws block contains the aws creds and it is available for jenkins pipeline
then aws ecr taken those creds for login for docker to creating a image


