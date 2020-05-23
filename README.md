# install jenkins by docker expose 2 port 8000 and 50000
docker run --name jenkins -d -v jenkins_home:/var/jenkins_home -p 8080:8080 -p 50000:50000 jenkins/jenkins:lts

# permission for uer
sudo chown $USER /var/run/docker.sock
sudo usermod -aG docker $USER
sudo systemctl restart docker

# get password of jenkins web
docker exec -it <container-ID> bash
cat /var/jenkins_home/secrets/initialAdminPassword
