Todo: Describe Scenario
`oc get images --as system:admin | grep blog-django-py`{{execute}}
`oc import-image sample:latest --from=openshiftkatacoda/blog-django-py --confirm`{{execute}}
`oc get images --as system:admin | grep blog-django-py`{{execute}}

# How do I get information about Image Streams?
oc describe is the universal way of getting a user-readable information about any object in the OpenShift cluster. This will give you general information about the Image Stream and detailed information about all the tags it is pointing to. In our example from the previous question we would invoke:
`oc describe is/sample`{{execute}}
to get all the information available about entire Image Stream,
`oc describe istag/sample:latest`{{execute}}
to get all the information available about particular Image Stream Tag.

# How do I add more tags to the current Image Stream?
To add a latest tag that points to one of the existing tags, you can use the oc tag command:
`oc tag sample:latest sample:test`{{execute}}
Examining the sample ImageStream with oc describe should assure us that we have exactly two tags, one (latest) pointing at the external docker image and another one (test) pointing to a different tag in the same Image Stream.

# How do I remove a tag from an Image Stream?
Eventually, you will want to remove old tags from your Image Stream, and yet again we are going to use oc tag for that particular use case:
`oc tag -d sample:test`{{execute}}