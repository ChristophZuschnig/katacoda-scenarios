# Objective of this step

Import the external sample application image to an Image Stream called sample.

## Step Two

First we want to verify that in the OpenShift Cluster no demo sample image is available:

`oc get images --as system:admin | grep blog-django-py`{{execute}}

After running the command no image of type blog-django-py is displayed.

## How do I create an Image Stream from an existing image

To create a new Image Stream named “sample” from an external Docker Registry with a single tag pointing to latest,
one needs to invoke following command:

`oc import-image sample:latest --from=openshiftkatacoda/blog-django-py --confirm`{{execute}} *mandatory*

Let us break this command into pieces:

sample:latest – sample is the new Image Stream that will be created as a result of this invocation. Additionally we are explicitly pointing that the imported image will be kept under the latest - Image Stream Tag of that Image Stream.

--from=openshiftkatacoda/blog-django-py – states what external image the Image Stream Tag will point to.

--confirm – informs the system that the python Image Stream should be created, if this is omitted and there is no python Image Stream, you will be presented with an error message.

At any point in time if you want to re-import the Image Stream, either entirely or just a single tag, use oc import-image and pass the name of the entire Image Stream or just a particular Image Stream Tag.

Now we want to verify that the sample application image is available:

`oc get images --as system:admin | grep blog-django-py`{{execute}}

After running the command the image is displayed.

## How do I get information about Image Streams

oc describe: is the universal way of getting a user-readable information about any object in the OpenShift cluster. This will give you general information about the Image Stream and detailed information about all the tags it is pointing to. In our example from the previous question we would invoke:

`oc describe is/sample`{{execute}}

to get all the information available about entire Image Stream,

`oc describe istag/sample:latest`{{execute}}

to get all the information available about particular Image Stream Tag.

## How do I add more tags to the current Image Stream

To add a latest tag that points to one of the existing tags, you can use the oc tag command:

`oc tag sample:latest sample:test`{{execute}}

Examining the sample ImageStream with oc describe should assure us that we have exactly two tags, one (latest) pointing at the external docker image and another one (test) pointing to a different tag in the same Image Stream.

`oc describe is/sample`{{execute}}

## How do I remove a tag from an Image Stream

Eventually, you will want to remove old tags from your Image Stream, and yet again we are going to use oc tag for that particular use case:

`oc tag -d sample:test`{{execute}}

`oc describe is/sample`{{execute}}
