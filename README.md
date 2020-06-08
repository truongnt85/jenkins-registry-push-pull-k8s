

# install jenkins by docker inside docker: map volume of Daemon host to Daemon container
docker run --name jenkins2 --privileged=true -d -v /var/run/docker.sock:/var/run/docker.sock -v jenkins_home:/var/jenkins_home  -p 8080:8080 -p 50000:50000 jenkins/jenkins:lts


# install jenkins by docker expose 2 port 8000 and 50000
docker run --name jenkins -d -v jenkins_home:/var/jenkins_home -p 8080:8080 -p 50000:50000 jenkins/jenkins:lts

# install jenkins by docker restart = always
docker run --name jenkins --restart=always --privileged=true -d -v /var/run/docker.sock:/var/run/docker.sock -v jenkins_home:/var/jenkins_home  -p 8080:8080 -p 50000:50000 jenkins/jenkins:lts



# login by user root to docker
docker exec -u 0 -it f3c92f941843  bash


# permission for uer
sudo chown $USER /var/run/docker.sock

sudo usermod -aG docker $USER
sudo systemctl restart docker

# get password of jenkins web from docker container
docker exec -it <container-ID> bash
cat /var/jenkins_home/secrets/initialAdminPassword
