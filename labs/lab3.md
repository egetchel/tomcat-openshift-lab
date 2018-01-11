Lab III - Interacting with OpenShift from JBoss Developer Studio
-------------------------
In this lab, we will now demonstrate one of many ways in which a Developer can interact with an OpenShift environment directly from JBoss Developer Studio.

First... a little workspace cleanup
* Stop the locally running Tomcat application. On the Servers tab, click the Tomcat instance and either hit the red stop button or right-click and Stop the server.
* Delete the SampleWebApp project from your workspace by right-clicking on the project in the Project Explorer and selecting "Delete". On the delete confirmation screen, Remember to select "Delete local disk contents" option. If the local disk contents remain, a Git collision will happen when the project is re-imported (you can alwasy manually delete the git repo off your local file system if this happens).

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
Note: if the "Save token" box is checked, it will attempt to save the token in a local secure store.
* If you look at your OpenShift Explorer tab, you will see a live link to your OpenShift environment. If you expand the caret, you will also see that you can interact with the application deployed on OpenShift, or OpenShift itself.
![](/images/openshift-explorer-connection-complete.png)  


At the beginning of this lab, we purposefully deleted the application from our workspace in order to demonstrate that the application and all the associated assets can be directly imported from OpenShift into JBoss Developer Studio.
* from the OpenShift Explorer tab, right-click on the Tomcat application deployed in OpenShift
* Select "Import Application"
* You can use the default values on the next screen

This will now execute a Git clone and bring a copy of the application assets local.  Once the import is complete, the application is now available to edit directly in JBoss Developer Studio, already hooked into the Git repository.


More interesting, you can continue to do development and testing locally (outside of OpenShift) on your local Tomcat instance.  After committing code, you can manually instruct OpenShift to execute a build and deploy, or set OpenShift via WebHooks to automatically build and deploy a new version of the application when code is committed.  

To configure the imported project to run against a local Tomcat instance, after the project is imported, simply do what was done in Lab 1 to associate your application to the local Tomcat instance:
* Right-click on your Tomcat server in the Servers tab
* Select "Add and Remove"
* Select the application that was just imported (Sample Web App)
* Click the "Add" button
* Click "Finish"
* Remember to also follow the steps to remove the document root
You can now interact with this application from a local (non-containerized) Tomcat application, just like what was done in Lab 1.

To trigger a manual rebuild and redeploy within OpenShift, simply expand the Tomcat Web App project, right-click on the tomcat-instance application, and select "Deploy Latest" 

We've just demonstrated complete round-tripping of a standard web application between traditional and containerized deploments of the same base application code. In the [next lab](/labs/lab4.md) we will show how Jenkins can be leveraged to manage the building and testing of the containerized application in OpenShift
