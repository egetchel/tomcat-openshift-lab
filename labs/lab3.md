Lab III - Interacting with OpenShift from JBoss Developer Studio
-------------------------
In this lab, we will now demonstrate one way in which a Developer can interact with an OpenShift environment directly from JBoss Developer Studio.

First... a little workspace cleanup
* Stop the locally running Tomcat application
* Delete the SampleWebApp project from your workspace by right-clicking on the project and selecting "Delete". On the delete confirmation screen, Remember to select "Delete local disk contents" option. If the local disk contents remain, a Git collision will happen when the project is re-imported.

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
![](/images/openshift-explorer-connection-complete.png)  
Note: if the "Save token" box is checked, it will attempt to save the token in a local secure store.

At the beginning of this lab, we purposefully deleted the application from our workspace in order to demonstrate that the application and all the associated assets can be directly imported into JBoss Developer Studio for editing.
* Right-click on the Tomcat Web App deployed in OpenShift
* Select "Import Application"
* You can use the default values on the next screen

This will now execute a Git clone and bring a copy of the application assets local.  Once the import is complete, the application is now available to edit directly in JBoss Developer Studio, already hooked into the Git repository.


More interesting, you can continue to do development locally (outside of OpenShift) and then committing the code, would trigger an OpenShift deployment. Afte the project is imported, simply do what was done in Lab 1 to associate your application to the local Tomcat instance:
* Right-click on your server
* Select "Add and Remove"
* Select the application that was just imported (Sample Web App)
* Click the "Add" button
* Click "Finish"
* Remember to also follow the steps to remove the document root
You can now interact with this application from a local (non-containerized) Tomcat application, just like what was done in Lab 1.

