##2)Copy jar file from Windows to ubuntu (do this in ubuntu console)
# locate window file inside ubuntu (folder below after /c/ might change
 cd /mnt/c/Users/carol/DevPro/IdeaProjects/Docker-Java-Udemy/UDocker-37-Fix-Docker-Assigment/
# copy/paste desire file (note: from and to paths might change) using the cp <copy-from-file> <paste-to-folder>
 cp /mnt/c/Users/carol/DevPro/IdeaProjects/Docker-Java-Udemy/UDocker-37-Fix-Docker-Assigment/spring-boot-web-0.0.1-SNAPSHOT.jar ~/docker/dockercontainers/UDocker-37-Fix-Docker-Assigment
# copy Dockerfile 
 cp /mnt/c/Users/carol/DevPro/IdeaProjects/Docker-Java-Udemy/UDocker-37-Fix-Docker-Assigment/Dockerfile ~/docker/dockercontainers/UDocker-37-Fix-Docker-Assigment

##4) build docker image (inside the folder where previously created Dockerfile is). It will create an image. You will get the image id, but we will use the tag to run it in next step
#Note: -t is for creating a tag. Command below defaults to the already created Dockerfile in the current folder
docker build -t spring-boot-docker-for-fix .

##5) run docker image
docker run -d -p 8080:8080 spring-boot-docker-for-fix 


##ANSWER HOW TO FIX Dockerfile
FROM centos

RUN sed -i -e "s|mirrorlist=|#mirrorlist=|g" /etc/yum.repos.d/CentOS-*
RUN sed -i -e "s|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g" /etc/yum.repos.d/CentOS-*
RUN yum install -y java

VOLUME /tmp
ADD /spring-boot-web-0.0.1-SNAPSHOT.jar myapp.jar
RUN sh -c 'touch /myapp.jar'
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/myapp.jar"]


