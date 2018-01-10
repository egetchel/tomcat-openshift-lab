Lab I - Simple Web Application
===============================

This lab is simply demonstrating how to set up your local development environment with JBoss Developer Studio / Eclipse, install Tomcat, configure JBDS to interact with Tomcat, and to import a sample Tomcat application which will be used in subsequent labs.

Install JBoss Developer Studio
---------------
JBoss Developer Studio (JBDS) is an Eclipse-based development environment with numerous productivity tools pre-installed. It can be downloaded from the Red Hat customer portal at [JBDS Download Link](https://access.redhat.com/jbossnetwork/restricted/listSoftware.html?downloadType=distributions&product=jbossdeveloperstudio&version=10.4.0).

If you already have Eclipse installed, you can also use the [community](https://tools.jboss.org/) version of the toolset in your copy of Eclipse.


1 - Import the Project
-------------------------
First, let's import a simple Tomcat web application into your development environment.  A simple web application is available in [Github](https://github.com/egetchel/SampleWebApp) for convenient access. Although not required, it is strongly recommended that you fork this project so that local changes can be committed and redeployments triggered via code commits.
 
* From the Project Explorer tab in JBDS, right-click and select "Import" from the menu.
* Select "Project from Git (with smart import)" and hit Next
![import](/images/import-git.png)
* Select "Clone URI" and hit Next
* Enter the repository URL to import and hit Next
![import](/images/import-git-repo-location.png)  
Note: Enter the URL of your Forked repository if you have forked it.
* Make sure the SampleWebApp is selected and hit Finish
![import](/images/import-specify-resources.png)

2 - Install and Register Tomcat Server with JBoss Developer Studio
-------------------------
Next, we will install Tomcat and configure JBoss Developer Studio to be able to interact with the server.
* Install [JBoss Web Server 3](https://access.redhat.com/jbossnetwork/restricted/listSoftware.html?product=webserver&downloadType=distributions) or community [Apache Tomcat](https://tomcat.apache.org/download-70.cgi).  Make note of where the binaries are installed.
* To allow JBDS to interact with the Tomcat server, we will create a new Server instance. In JBDS, find the Servers tab (towards the bottom of the screen), and click the link to create a new server. If a server instance already exists, simply right-click on an empty area and select "New" -> "Server"
![create](/images/create-new-server.png)
* This will bring up a list of server runtimes that JBDS can manage. In the Apache section, select Tomcat v7.0 Server and select "Next"  
![create](/images/create-tomcat-instance.png)
* If no existing Tomcat runtime environments have been registered with JBDS, the next window will prompt for the Tomcat installation location.  Select "Browse" and navigate to the root install folder of Tomcat and select "Next"
![create](/images/create-tomcat-install-directory.png) 
* In the Add and Remove window, add the SampleWebApp project that was previously imported to the Tomcat server and select "Finish"  
![create](/images/create-add-web-app.png)

The server should now show in the Servers tab at the bottom of the screen.

3 - Update the Document Root
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

4 - Start the Tomcat Server
-------------------------

* Either right-click on the Tomcat server in the Servers tab and select Start, or click the green play button on the Servers tab. 
* Note, there may be errors in the Console, but these can be ignored.
* Using a web browser, [Navigate](http://localhost:8080) to the sample web application

So we've simply imported a simple web application into JBoss Developer Studio and deployed it to a local Tomcat instance.  Nothing special there.  Now, let's go through a few scenarios where we can automatically containerize the application and deploy it on a PaaS in [lab2](/labs/lab2.md).
