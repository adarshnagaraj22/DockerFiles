FROM ubuntu:latest
MAINTAINER Adarsh Nagaraj <adarshgowda4@gmail.com>

# Updating and Installing Java openjdk, wget, curl, maven and git packages
RUN apt-get -y update && apt-get install -y curl wget openjdk-8-jdk maven git

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

# Cloning Java application from github
RUN git clone https://github.com/adarshnagaraj22/Java-Mysql-Simple-Login-Web-application.git /tmp/project

# Working directory for packaging Java application
WORKDIR /tmp/project

# Building Java application using maven
RUN mvn package

# Copying war file to tomcat webapps directory
RUN cp /tmp/project/target/LoginWebApp.war /usr/local/tomcat/webapps/LoginWebApp.war

# Starting tomcat
CMD /usr/local/tomcat/bin/catalina.sh run
