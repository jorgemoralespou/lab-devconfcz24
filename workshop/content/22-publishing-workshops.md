---
title: Publishing Workshops
---

To deploy the workshop we first need to publish it to a place where Educates
will be able to download the workshop files at runtime.

Educates supports different mechanisms for hosting of the workshop files,
including:

* Hosting workshop files as an OCI image on an image registry.
* Hosting workshop files as a tar/zip archive on a web server.
* Hosting workshop files on a hosted Git repository (eg., GitHub).

In other words, unlike many other SaaS based training platforms, you are not
required to edit your workshop content in the platforms web interface. Instead,
you can work on your workshop content locally and host your workshop files
separately, with Educates downloading the workshop files when required.

Of the mechanisms listed above, the recommended method is to publish workshop
files as an OCI image to an image registry. The standard workflow for authoring
workshops using the CLI and a local Educates cluster is tailored to using this
mechanism.

To publish our workshop, first change to the directory containing the workshop
files:

```terminal:execute
command: cd ~/lab-demo-workshop
```

and run the following command to publish the workshop files.

```terminal:execute
command: educates publish-workshop
```

What is being done here is that the workshop files from the current directory
are being bundled up into an OCI image and pushed to a local image registry
hosted at `localhost:5001`. This image registry was automatically created for
you as part of this workshop session. If you used the CLI to create a local
Kubernetes cluster running Educates, a local image registry would similarly be
automatically deployed for you and integrated with the cluster. The process here
in this workshop session thus mimics what you can expect if using the Educates
CLI from your own computer using a local Kubernetes cluster.

If not using a local Kubernetes cluster and you were instead using a hosted
Kubernetes cluster, instead of using a local image registry you would need to
specify a separate image registry to use which is visible to the hosted
Kubernetes cluster.

If using GitHub to host workshops, you could use GitHub container registry, and
to make that process simpler Educates provides a pre-packaged GitHub action
which can be used to automate publishing of workshops.