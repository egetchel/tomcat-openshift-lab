Openshift Developer Workflow Labs for Java Based Web Applications
===============================
Author: Eric Getchell   
Level: Intermediate  
Technologies: OpenShift, JBoss Developer Studio, Tomcat, Jenkins,  Git, Containers  
Summary: Step through a simple workflow that demonstrates portability between containerized and non-containerized runtimes with a sample Tomcat application.  Learn how to leverage Source 2 Image (S2I) for containerizing existing applications and add Jenkins into your application build and test lifecycles 
Target Products: JBoss JWS, OpenShift, JBoss Developer Studio, Jenkins  
Source: <https://github.com/egetchel/tomcat-openshift-lab>  

What is it?
-----------

This lab will demonstrate typical developer workflow for working with Java web applications in a both a traditional and containerized format.  The labs start with importing of a simple Java web application into JBoss Developer Studio, deploying on a local Tomcat instance, and then showing how this same web application can be seamlessly containerized and deployed into OpenShift, Red Hat's container management platform. Finally, we will show how a containerized version of Jenkins can be leveraged to manage the build and test lifecycle of your application within OpenShift.


System requirements
-------------------

You will need Java 8.0 (Java SDK 1.8) or later, Maven 3.1.1 or later, JBoss Developer Studio 10, Tomcat 7 or 8, and an instance of OpenShift.

Labs
----
* [lab1 - Environment Setup and application import](/labs/lab1.md)
* [lab2 - Containerizing the Tomcat application](/labs/lab2.md)
* [lab3 - JBoss Developer Studio to OpenShift workflow](/labs/lab3.md)
* [lab4 - Adding Jenkins](/labs/lab4.md)