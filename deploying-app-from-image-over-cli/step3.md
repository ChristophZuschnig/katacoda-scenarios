# Objective of this step

After importing the sample image openshiftkatacoda/blog-django-py to an Image Stream named *sample*, we will create an application with this image.

## Check if image is available for creation an application

The name of the image you used previously was *openshiftkatacoda/blog-django-py* and we imported it to the Image Stream *sample*. If you have been given the name of an Image Stream to deploy and want to verify that it’s valid from the command line, you can use the oc new-app --search command. For this image, run:

`oc new-app --search sample`{{execute}}

You see that the image stream is found. This confirms that the image stream is found in the internal OpenShift registry.

To create and deploy the image, you can run the following command:

## Create and deploy the Image Stream

`oc new-app sample`{{execute}} *mandatory*

OpenShift will assign a default name based on the name of the image, in this case, sample. You can specify a different name to be given to the application, and the resources created, by supplying the --name option along with the name you wish to use as an argument. Keep in mind that changing the name will change the value of the app label and when deleting the application you will then need to use this name. You can see that the resources deploymentconfig and service 'sample' was created too.

As with deploying an existing container image from the web console, it’s not exposed outside of the OpenShift cluster by default. To expose the application created so it’s available outside of the OpenShift cluster, you can run this command:

`oc expose service/sample`{{execute}} *mandatory*

## Visit the sample application

Switch to the OpenShift web console to verify that the application has been deployed. Click on the URL displayed on the Overview page for the project to visit the application.

This will log you in using the credentials:

    Username: developer
    Password: developer

Alternatively, to view the hostname assigned to the route created from the command line, you can run this command:

`oc get route/sample`{{execute}}
