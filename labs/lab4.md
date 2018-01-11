Lab IV - Adding Jenkins
-------------------------
This lab will quickly show how Jenkins can be integrated into your project. This lab will be done from within the Web Console of OpenShift.  This will be a brief introduction with the intent in getting a minimal Jenkins install working.

* Next to the project name on the top of the OpenShift Web Console is a drop down titled "Add to Project".  
![](/images/jenkins-add-to-project.png)
Select the "Browse Catalog Option"
* Scroll to the bottom of this window and in the Technologies section, select "Continuous Integration & Deployment
![](/images/jenkins-select-ci.png)
* Select the "Jenkins (Persistent) option on the next screen. *Note, depending on your OpenShift environment, the Jenkins image may need to be installed with a persistent volume.*
* On the next screen, leave all values defaulted and click the "Create" button at the bottom
![](/images/jenkins-default-options.png)
* You can ignore the warning that is displayed regarding the permission grant. Hit the "Create Anyway" button
* A new Jenkins instance will be added to your project
* If you hit the "Continue to Overview" link, you will now see your project has both a Tomcat application instance and a Jenkins application instance running.
![](/images/jenkins-added-to-project.png)
* We now have a working Jenkins instance.  Let's log into it and have it manage our application builds
* Select the link off the Overview screen that will take you to the familiar Jenkins user interface.
![](/images/jenkins-navigate-to-server.png)
* The first time you access Jenkins, it will ask to authorize through OpenShift.  This is because when the image was created, one of the options was how to authorize the Jenkins user. 
* On the Jenkins Home page, click "New Item"
* "Enter a name ("jenkins-tomcat-webapp), click "Freestyle Project", and select "OK" at the bottom of the screen.
![](/images/jenkins-new-item.png)
* We now have an empty Jenkins project with the OpenShift pipeline plugins available to configure how the build will be managed.
    * Remove the "Restrict where this project can be run" checkbox *(note - is this needed?)*
    * Under Source Code Management, select Git and enter the URL to your repository
    * Next we will define the steps that Jenkins will take to build the application.  We will be working against the actual Tomcat web application in our Project (which was called "tomcat-instance" earlier in the labs).  On the Build section, enter the following:
        * Click the "Add build step" and select Trigger OpenShift Build - enter "tomcat-instance" as the name of the Build Config to tigger.
        * Click the "Add build step" and select Trigger OpenShift Deployment - enter "tomcat-instance" as the Deployment Config
        * Click the "Add build step" and select Scale OpenShift Deployment - enter "tomcat-instance" as the Deployment Config and "1" as the number of replicas  
    ![](/images/jenkins-build-config.png)    
    * We have just defined a Jenkins managed job to build a web application, and  have OpenShift containerize and deploy the application.  Click the "Save" button.
    * On the left-hand navigation panel, Click "Build Now"
    * Navigate back to your OpenShift console, and on the Application Overview, you will see a new version of the tomcat-instance (Tomcat web application being built)
    
Other steps to the build process can be added, such as automatically building when code is committed, executing tests, or handing the process off to another Jenkins job.
