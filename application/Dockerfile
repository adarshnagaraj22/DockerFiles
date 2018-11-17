FROM ubuntu:latest
MAINTAINER Adarsh Nagaraj <adarshgowda4@gmail.com>

# Updating and Installing Java openjdk, wget and curl packages
RUN apt-get -y update && apt-get install -y curl wget openjdk-8-jdk

# Create directory for Tomcat Installation
RUN mkdir /usr/local/tomcat

# Downloading tomcat 8 tar file to tmp directory
RUN wget http://mirrors.estointernet.in/apache/tomcat/tomcat-8/v8.0.53/bin/apache-tomcat-8.0.53.tar.gz -O /tmp/tomcat.tar.gz

# Untar the downloaded Tomcat file
RUN cd /tmp && tar xvfz tomcat.tar.gz

# Copy the tomcat files to the tomcat directory
RUN cp -Rv /tmp/apache-tomcat-8.0.53/* /usr/local/tomcat/

# Exposing port 8080 of the tomcat container
EXPOSE 8080

# Updating and Installing Maven and git for building java application
RUN apt-get -y update && apt-get install -y maven git

# Cloning Java application from github
RUN git clone https://github.com/arjunyadav123/registration-login-java-xml-maven-jsp-mysql.git /tmp/project

# Working directory for packaging Java application
WORKDIR /tmp/project

# Building Java application using maven
RUN mvn package

# Copying war file to tomcat webapps directory
RUN cp /tmp/project/target/LoginWebApp.war /usr/local/tomcat/webapps/LoginWebApp.war

# Starting tomcat
CMD /usr/local/tomcat/bin/catalina.sh run
