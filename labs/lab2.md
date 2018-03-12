Lab II - Containerize the Tomcat Application
-------------------------
In this lab, we will automatically containerize the web application from the previous lab and deploy it as a Docker image into OpenShift.  This lab emphasizes the Source 2 Image (S2I) process that can be leveraged to automatically containerize existing web applications into Docker images using a standardized build process and leveraging supported base images.
 
* Log into OpenShift.  If no Projects exist, then the Create Project button will be available
![create](/images/openshift-home-page.png)
* In the upper-right hand section of the screen, click Create Project to launch the wizard used to create a Project and associate applications to it.  A Project in OpenShift is a way to group individual applications. On the Create Project screen, enter a project name and display name for the project.  
![create](/images/openshift-create-project.png)  
* After entering field values, click the "Create" button. The screen will reflect the newly created Project  
![create](/images/openshift-project-created.png)
* Click the Project name "Tomcat Web App" to navigate into the Project you just created.  You are now in an empty Project.  
![create](/images/openshift-empty-project.png)
* Now that the Project is created, we will add the Tomcat web application itself. Clicking the "Browse Catalog" button will show the various technologies that OpenShift can containerize out of the box.  The screen that is displayed allows for filtering.  In this case, I selected "Languages"
![create](/images/openshift-language-filter.png)
* Click the "Java" button to bring up the next screen.
* Next, we can specify the type of Java application we want to containerize and deploy. You can see various default offerings from a simple Java main (OpenJDK), to a fully featured JEE Application Server (Red Hat JBoss EAP) and Tomcat to name a few.  
![create](/openshift-select-language.png)
Select the Red Hat JBoss Web Server (Tomcat) button.
* This will bring up a wizard to configure the Tomcat portion of your project  
![create](/images/openshift-create-tomcat-webapp-step-1.png)
* Click the "Next" button  
* This screen allows individual configurations based on the type of image you are using. For example, if this image also had a database component, you would be able to supply a username and password pair here.  Use the Git URL of your repository cloned in previous steps (or https://github.com/egetchel/SampleWebApp/ if you want to quickly try a sample application).   
Typically, default values can be used, but there are a couple bugs (which may be fixed in your environment) around the default values.
- Git Reference : Remove any value
- Context Directory : Remove any value
The remaining values can remain as-is  
![create](/images/openshift-create-tomcat-webapp-step-2.png) 
* Hit the "Create" button which will show that the applicaiton has been created.
![create](/images/openshift-create-tomcat-webapp-step-3.png) 
* Finally, we provide a name for the actual Tomcat resource as well as where the source code of our web application resides.  Use the Git URL of your repository used in previous steps (or https://github.com/egetchel/SampleWebApp/ if you want to quickly try a sample application).  
* Click the "Continue to overview" link
* After a minute or so, you should see a screen that looks something like the following:
![create](/images/openshift-application-overview.png)  
Clicking on the link (red arrow above) will open a new browser tab and navigate you to your running web application. *Note, the URL will be specific to your OpenShift environment.*

So, what just we just do?  Essentially, we have instructed OpenShift to compile our application, use a base builder image (consisting of a JDK and Tomcat), and layer our application in as a standard Docker image.

In the [next lab](/labs/lab3.md) we will demonstrate how we can interact with the OpenShift environment directly from JBoss Developer Studio.