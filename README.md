# Apache Tomcat Deployment Guide

This guide provides step-by-step instructions on how to install and deploy an application in Apache Tomcat.

## Table of Contents

- [Introduction](#introduction)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Deployment](#deployment)
- [Accessing the Application](#accessing-the-application)
- [Conclusion](#conclusion)

## Introduction

Apache Tomcat is an open-source web server and Java Servlet container that allows you to run Java-based web applications. This guide will walk you through the process of installing Tomcat and deploying your application.

## Prerequisites

Before proceeding with the installation, ensure that you have the following prerequisites:

- Ubuntu operating system (or compatible Linux distribution. If possible then use AWS instances) 
- Java Development Kit (JDK) 11 or later
- Maven (for building the application)

## Installation

1. Open a terminal.
2. Change to the `/opt` directory:
cd /opt


3. Download the Tomcat installation package using `wget`:
sudo wget https://archive.apache.org/dist/tomcat/tomcat-9/v9.0.65/bin/apache-tomcat-9.0.65.tar.gz
 
 
4. Extract the downloaded package:
sudo tar -xvf apache-tomcat-9.0.65.tar.gz


5. Configure the Tomcat user roles by editing the `tomcat-users.xml` file:
cd /opt/apache-tomcat-9.0.65/conf
sudo vi tomcat-users.xml


Add the following line at the end (2nd-last line) of the file:
 ```<user username="admin" password="admin1234" roles="admin-gui, manager-gui"/>```

6. Create symbolic links for starting and stopping Tomcat:
   ```
   sudo ln -s /opt/apache-tomcat-9.0.65/bin/startup.sh /usr/bin/startTomcat
   sudo ln -s /opt/apache-tomcat-9.0.65/bin/shutdown.sh /usr/bin/stopTomcat
   ```
7. Edit the context.xml files for the Manager and Host Manager applications:
   ```sudo vi /opt/apache-tomcat-9.0.65/webapps/manager/META-INF/context.xml```
   Comment out the following line by adding `<!--` at the beginning and `-->` at the end:
   ```
   <!-- Valve className="org.apache.catalina.valves.RemoteAddrValve"
     allow="127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1" /> -->
   ```
   ```
   sudo vi /opt/apache-tomcat-9.0.65/webapps/host-manager/META-INF/context.xml
   ```
   Comment out the same line as above.
Deployment
Install Java 11 and Maven (if not already installed):

sudo apt-get update -y
sudo apt install openjdk-11-jre -y
sudo apt-get install maven -y
Stop the Tomcat server:

sudo stopTomcat
Start the Tomcat server:

sudo startTomcat
Clone your application repository:


git clone https://github.com/soumyadip007/E-Medical-System-Web-Project-Using-Spring-Boot-Security-JPA-Rest-Thymeleaf-HQL.git
Build the application using Maven:


cd your-application
mvn clean package
Copy the built application (WAR file) to the Tomcat webapps directory:


sudo cp target/your-application.war /opt/apache-tomcat-9.0.65/webapps
Change the owner of the Tomcat directory to the current user (optional, if deploying as non-root):


sudo chown -R ubuntu /opt/apache-tomcat-9.0.65
Accessing the Application
Once the application is deployed, you can access it using the following URL:


http://localhost:8080/your-application
Replace your-application with the appropriate context path or name of your application. 
e.g If using AWS and your ip is 13.09.90.2 then the URL will look like http://13.09.90.2:8080/E-Medical-System-Web-Project-Using-Spring-Boot-Security-JPA-Rest-Thymeleaf-HQL

Conclusion
In this guide, we have covered the process of installing and deploying an application in Apache Tomcat. By following the steps outlined, you can set up a Tomcat server, configure user roles, and deploy your Java-based web application.

We started by installing the necessary prerequisites, including the Ubuntu operating system, JDK, and Maven. Then, we proceeded with the installation of Apache Tomcat, configuring user roles, and creating symbolic links for convenient startup and shutdown of the server.

Next, we covered the deployment process, including cloning the application repository, building the application using Maven, and copying the generated WAR file to the Tomcat webapps directory. Additionally, we provided instructions on changing the owner of the Tomcat directory if deploying as a non-root user.

Finally, we concluded with information on how to access the deployed application through the appropriate URL.

By following this guide, you can successfully deploy your Java web application using Apache Tomcat, a reliable and widely used web server and servlet container.

Remember to customize the instructions based on your specific application and deployment requirements.


Feel free to use this README file template for your GitHub repository
