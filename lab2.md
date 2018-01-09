Lab II - Containerize the Tomcat Application
-------------------------
In this lab, we will use our standard web application and automatically containerize the application and deploy it as a Docker image into OpenShift.  This lab emphasizes the Source 2 Image (S2I) process that can be leveraged to automatically convert existing web applications into Docker images using a standardized build process and leveraging supported base images.
 
* Log into OpenShift.  If no Projects exist, then the Create Project button will be available
![create](/images/openshift-home-page.png)
* Click Create Project to launch the wizzard used to quickly create a Project and associate applications to it.  A Project in OpenShift is a way to group individual applications. On the Create Project screen, enter a project name and display name for the project.  
![create](/images/openshift-create-project.png)  
After entering field values, click the "Create" button.
* Now that the Project is created, we will add the Tomcat web application itself.  The next screen allows you to add various technologies in a containerized fashion.  
![create](/images/openshift-add-java-application.png)
Click the Java button to bring up the next screen.
* Next, we can specify the type of Java application we want to containerize and deploy.
![create](/images/openshift-create-tomcat-app.png)  
Select the Red Hat JBoss Web Server (Tomcat) button.
* The next screen shows all avaiable Tomcat images. Choose any of the Tomcat 7 images.
![create](/images/openshift-specify-tomcat-version.png)
* Finally, we provide a name for the actual Tomcat resource and where the source code of our web application resides.  Use the Git URL of your repository used in previous steps.  
![create](/images/openshift-assicate-git-repo.png)
* Clicking on the "Create" button will start the assembly process. The next screen provides some overview information on the container image
![create](/images/openshift-application-created.png)
* Click the "Continue to overview" link
* After a minute or so, you should see a screen that looks something like the following:
![create](/images/openshift-application-overview.png)
* So, what just we just do?  Essentially, we have instructed OpenShift to compile our application, use a base builder image (consisting of a JDK and Tomcat), and layer our application in as a standard Docker image.
