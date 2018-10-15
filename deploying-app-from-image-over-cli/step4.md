# Objective of this step

After deploying the sample image *sample*, we will will custimze the application by setting environment variables and Config Maps.

## Via environment variables

To make it easy to demonstrate green/blue or a/b deployments, it is possible to modify the appearance of the blog application by setting environment variables. These are:

    BLOG_SITE_NAME - Sets the title for pages.
    BLOG_BANNER_COLOR - Sets the color of the page banner.

To set environment variables from the command line, you can run:

`oc set env dc/sample BLOG_BANNER_COLOR=blue`{{execute}}

`oc set env dc/sample BLOG_SITE_NAME='BLOG Sample Blog'`{{execute}}

Under the title on each page, the host name for the pod handling the request is also shown if disabling sticky sessions on routing, or using curl to show how requests or different users are automatically load balanced across instances when scaled up.

## Via Config maps

In addition to being able to perform customisations using environment variables, use of a config map is also supported.

The config map should be defined as a JSON data file. For example, a blog.json file is available for demonstration.

~~~~json
{
   "BLOG_SITE_NAME": "OpenShift Blog",
   "BLOG_BANNER_COLOR": "black"
}
~~~~

The config map can be created using the command:

`oc create configmap blog-settings --from-file=blog.json`{{execute}}

and then mounted into the container using:

`oc set volume dc/sample --add --name settings --mount-path /opt/app-root/src/settings --configmap-name blog-settings -t configmap`{{execute}}

Even if a config map is used, environment variables, if defined for the same settings, will take precedence. We will unset the environment variable BLOG_BANNER_COLOR

`oc set env dc/sample BLOG_BANNER_COLOR-`{{execute}}

so now the value of the ConfigMap will taken.

