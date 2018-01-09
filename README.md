Openshift Developer Workflow Labs for Java Web Applications
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


Install JBoss Developer Studio
---------------
JBoss developer studio is an Eclipse-based development environment with numerous tools pre-installed. It can be downloaded from the Red Hat customer portal at [JBDS Download Link](https://access.redhat.com/jbossnetwork/restricted/listSoftware.html?downloadType=distributions&product=jbossdeveloperstudio&version=10.4.0).


Import the Project
-------------------------
First, let's import a simple Tomcat web application.  The project is in [Github](https://github.com/egetchel/SampleWebApp) for convenient access. It is strongly recommended that you Fork this project so that local changes can be committed and redployments triggered.
 
* From the Project Explorer menu, right-click and select "Import"
* Select "Project from Git (with smart import)" and hit Next
![import](/images/import-git.png)
* Select "Clone URI" and hit Next
* Enter the repository URL to import and hit Next
![import](/images/import-git-repo-location.png)  
Note: Enter the URL of your Forked repository.
* Make sure the SampleWebApp is selected and hit Finish
![import](/images/import-specify-resources.png)

Install and Register Tomcat Server with JBoss Developer Studio
-------------------------
Next, we will install Tomcat and configure JBoss Developer Studio to be able to interact with the server.
* Install [JBoss Web Server 3](https://access.redhat.com/jbossnetwork/restricted/listSoftware.html?product=webserver&downloadType=distributions) or community [Apache Tomcat](https://tomcat.apache.org/download-70.cgi).  Make note of where the binaries are installed.
* To allow JBDS to interact with the Tomcat server, we will create a new Server instance. In JBDS, find the Servers tab (towards the bottom of the screen), and click the link to create a new server. If a server instance already exists, simply right-click on an empty area and select "New" -> "Server"
![create](/images/create-new-server.png)
* This will bring up a list of runtimes that JBDS can manage. In the Apache section, select Tomcat v7.0 Server and select "Next"  
![create](/images/create-tomcat-instance.png)
* If no existing Tomcat runtime environments have been registred with JBDS, the next window will prompt for the Tomcat installation location.  Select "Browse" and navigate to the root install folder of Tomcat and select "Next"
![create](/images/create-tomcat-install-directory.png) 
* In the Add and Remove window, add the SampleWebApp project that was previously imported to the Tomcat server and select "Finish"  
![create](/images/create-add-web-app.png)

The server should now show in the Servers tab at the bottom of the screen.

Update the Document Root
-------------------------
Note: This step is a workaround. The pom.xml is configured to create a web application as ROOT.WAR, which normally instructs Tomcat to deploy the application without a context root. In this case, Eclipse is generating an application with a context root of 'ROOT'.  This one-time step will eliminate this incorrect context root.
* Open the Server configuration by double-clicking on the Tomcat server in the Servers tab.
* On the bottom of the Tomcat configuration screen are two tabs labeled 'Overview' and 'Modules'. Select the Modules tab.
* You will see the SampleWebApp application. Click the 'Edit' button
![modify](/images/tomcat-modify-context-root.png)
* Remove the value '/ROOT' from the Path attribute  
![remove](/images/tomcat-remove-context-root.png)
* Click OK
* Save the configuration changes (File -> Save or hit the disk icon).

Start the Tomcat Server
-------------------------

* Either right-click on the Tomcat server in the Servers tab and select Start, or click the green play button on the Servers tab. 
* Note, there may be errors in the Console, but these can be ignored.
* Using a web browser, [Navigate](http://localhost:8080) to the sample web application

Great - so we've simply imported a simple web application into JBoss Developer Studio and deployed it to a local Tomcat instance.  Nothing special there.  Now, let's go through a few scenarios where we can automatically containerize the application and deploy it on a PaaS.
 
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

Lab III - Interacting with OpenShift from JBoss Developer Studio
-------------------------
In this lab, we will now demonstrate one way in which a Developer can interact with an OpenShift environment directly from JBoss Developer Studio.

First... a little workspace cleanup
* Stop the locally runnint Tomcat application
* Delete the SampleWebApp project from your workspace. Remember to select "Delete local disk contents" option.

Now, let's see how we can interact with OpenShift directly from JBoss Developer Studio
* In JBoss Developer Studio, on the bottom tab bar, select "OpenShift Explorer"
![](/images/openshift-explorer-new-connection.png)  
and select "New Connection Wizard"
* The first screen of the wizard will allow you to retrieve an access token to interact with the OpenShift environment.  Enter the URL of your OpenShift environment and select the "retrieve" link.
![](/images/openshift-explorer-new-token-start.png)
* After clicking the "retrieve" link, you will be prompted for your username and password for the OpenShift environment.
* Upon authenticating, a screen showing your authorization token is displayed
![](/images/openshift-explorer-auth-token.png)  
* Simply hit "Close" and you will see the token automatically populated for you
![](/images/openshift-explorer-auth-token-complete.png)
* If you look at your OpenShift Explorer tab, you will see a live link to your OpenShift environment. If you expand the carret, you will also see that you can interact with the application deployed on OpenShift
![](/images/openshift-explorer-connection-complete.jpg)

We purposefully deleted the application from our workspace in order to demonstrate that the application and all the associated assets can be directly imported into JBoss Developer Studio for editing.
* Right-click on the Tomcat Web App deployed in OpenShift
* Select "Import Application"
* You can use the default values on the next screen
Once complete, the application is now available to edit directly in JBoss Developer Studio, already hooked into the Git repository.
You can fully interact with the OpenShift instance directly from your JBoss Developer Studio Environment

Lab IV - Adding Jenkins
-------------------------
This lab will quickly show how Jenkins can be integrated into your project.
* Next to the project name on the top of the OpenShift Web Console is a drop down titled "Add to Project".  
![](/images/jenkins-add-to-project.png)
Select the "Browse Catalog Option"
* Scroll to the bottom of this window and in the Technologies section, select "Continuous Integration & Deployment
![](/images/jenkins-select-ci.png)
* Select the "Jenkins (Persistent) option on the next screen
* On the next screen, leave all values defaulted and click the "Create" button at the bottom
![](/images/jenkins-default-options.png)
* You can ignore the warning that is displayed regarding the permission grant. Hit the "Create Anyway" button
* A new Jenkins instance will be added to your project
* If you hit the "Continue to Overview" link, you will now see your Application Overivew screen with the Jenkins instance added
![](/images/jenkins-added-to-project.png)
* We now have a working Jenkins instance.  Let's log into it and have it manage our application builds
* Select the link off the Overview screen that will take you to the familiar Jenkins user interface.
* The first time you access Jenkins, it will ask to authorize through OpenShift.  This is because when the image was created, one of the options was how to authorize the Jenkins user. 
* On the Jenkins Home page, click "New Item"
* "Enter a name ("jenkins-tomcat-webapp), "Freestyle Project", and select "OK" at the bottom of the screen.
![](/images/jenkins-new-item.png)
* We now have an empty Jenkins project with the OpenShift pipeline plugins available to dictate how the build will be managed.
    * Remove the "Restrict where this project can be run" checkbox (note - is this needed?)
    * Under Source Code Management, select Git and enter the URL to your repository
    * Next we will define the steps that Jenkins will take to build the application.  We will be working against the actual Tomcat web application in our Project (which was called "tomcat-instance" earlier in the labs).  On the Build section, enter the following:
        * Click the "Add build step" and select Trigger OpenShift Build - enter "tomcat-instance" as the name of the Build Config to tigger.
        * Click the "Add build step" and select Trigger OpenShift Deployment - enter "tomcat-instance" as the Deployment Config
        * Click the "Add build step" and select Scale OpenShift Deployment - enter "tomcat-instance" as the Deployment Config and "1" as the number of replicas
    * We have just defined a Jenkins managed job to build a web application, and  have OpenShift containerize and deploy the application.  Click the "Save" button.
    * On the left-hand navigation panel, Click "Build Now"
    * Navigate back to your OpenShift console, and on the Application Overview, you will see a new version of the tomcat-instance (Tomcat web application being built)

Other steps to the build process can be added, such as automatically building when code is comitted, executing tests, or handing the process off to another Jenkins job.
