Openshift Developer Workflow Labs for Java Based Web Applications
===============================
Author: Eric Getchell   
Level: Intermediate  
Technologies: Tomcat, Servlet, OpenShift, JBoss Developer Studio, Git, Containers  
Summary: Demonstrate importing of a simple, traditional, web application into JBoss Developer Studio, deploying on a local Tomcat instance, and then leveraging Source 2 Image to seamlessly containerize the application and deploy the image into OpenShift.  
Target Products: JBoss JWS, OpenShift, JBoss Developer Studio  
Source: <https://github.com/egetchel/SampleWebApp/>  

What is it?
-----------

Step through a simple workflow that demonstrates portability between containerized and non-containerized runtimes with a sample Tomcat application.  Learn how to leverage Source 2 Image (S2I) for containerizing existing applications)


System requirements
-------------------

The application in this project is designed to be run as a standalone Tomcat applcation, with JBoss Developer Studio, and as a container image within an Openshift instance.

You will need Java 8.0 (Java SDK 1.8) or later, Maven 3.1.1 or later, JBoss Developer Studio 10, Tomcat 7 or 8, and an instance of OpenShift.

* ![lab1 - Import the Tomcat application](lab1.md)
* ![lab2 - Containerize the Tomcat application](/lab2.md)
* ![lab3 - Hook JBDS to OpenShift](/lab3.md)
* ![lab4 - Add Jenkins](/lab4.md)