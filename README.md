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




1. Make sure you have started the JBoss EAP server as described above.
2. Open a command prompt and navigate to the root directory of this quickstart.
3. Type this command to build and deploy the archive:

        mvn clean install wildfly:deploy

4. This will deploy `target/jboss-helloworld.war` to the running instance of the server.


Access the application 
---------------------

The application will be running at the following URL: <http://localhost:8080/jboss-helloworld>. 


Undeploy the Archive
--------------------

1. Make sure you have started the JBoss EAP server as described above.
2. Open a command prompt and navigate to the root directory of this quickstart.
3. When you are finished testing, type this command to undeploy the archive:

        mvn wildfly:undeploy


Run the Quickstart in Red Hat JBoss Developer Studio or Eclipse
-------------------------------------
You can also start the server and deploy the quickstarts or run the Arquillian tests from Eclipse using JBoss tools. For general information about how to import a quickstart, add a JBoss EAP server, and build and deploy a quickstart, see [Use JBoss Developer Studio or Eclipse to Run the Quickstarts](https://github.com/jboss-developer/jboss-developer-shared-resources/blob/master/guides/USE_JBDS.md#use-jboss-developer-studio-or-eclipse-to-run-the-quickstarts) 


Debug the Application
------------------------------------

If you want to debug the source code of any library in the project, run the following command to pull the source into your local repository. The IDE should then detect it.

        mvn dependency:sources

