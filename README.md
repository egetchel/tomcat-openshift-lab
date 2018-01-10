Openshift Developer Workflow Labs for Java Based Web Applications
===============================
Author: Eric Getchell   
Level: Intermediate  
Technologies: OpenShift, JBoss Developer Studio, Tomcat, Web Applications,  Git, Containers  
Summary: Step through a simple workflow that demonstrates portability between containerized and non-containerized runtimes with a sample Tomcat application.  Learn how to leverage Source 2 Image (S2I) for containerizing existing applications)  
Target Products: JBoss JWS, OpenShift, JBoss Developer Studio  
Source: <https://github.com/egetchel/tomcat-openshift-lab>  

What is it?
-----------

This lab will demonstrate typical developer workflow for working with Java web applications in a containerized format.  The labs start with importing of a simple Java web application into JBoss Developer Studio, deploying on a local Tomcat instance, and then showing how this same web application can be seamlessly containerized and deployed into OpenShift, Red Hat's container management platform.


System requirements
-------------------

You will need Java 8.0 (Java SDK 1.8) or later, Maven 3.1.1 or later, JBoss Developer Studio 10, Tomcat 7 or 8, and an instance of OpenShift.

Labs
----
* [lab1 - Import the Tomcat application](/labs/lab1.md)
* [lab2 - Containerize the Tomcat application](/labs/lab2.md)
* [lab3 - Hook JBDS to OpenShift](/labs/lab3.md)
* [lab4 - Add Jenkins](/labs/lab4.md)