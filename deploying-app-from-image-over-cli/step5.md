# Objective of this step

Reconfigure the blog sample to use an persistence Datebase. A PostgreSQL database can be used to add persistence for blog posts.

## Deploy a PostgreSql Database

To deploy a PostgreSQL database from the command line, you can run:

`oc new-app postgresql-persistent --name sample-database --param DATABASE_SERVICE_NAME=sample-database --param POSTGRESQL_USER=sampledb --param POSTGRESQL_PASSWORD=sampledb --param POSTGRESQL_DATABASE=sampledb`{{execute}}

To re-configure the blog application to use the database, you need to set the DATABASE_URL environment variable for the blog application.

`oc set env dc/sample DATABASE_URL=postgresql://sampledb:sampledb@sample-database:5432/sampledb`{{execute}}

As a separate service is used for the database, it is necessary to manually setup the database the first time. This requires logging into the pod and running a setup script.

To run the setup script from the command line, you can run:

`POD='oc get pods --selector app=blog-from-source-py -o name'`{{execute}}

`oc rsh $POD scripts/setup`{{execute}}

The setup script will initialize the database tables and then prompt you for details of an initial account to setup.

You can login to the blog application by clicking on the person icon top right of the blog application web page. Then click the plus icon top right to add a new post.

The blog posts title and text content should now survive a restart of the container. Any uploaded image will still be lost at this point on a restart.