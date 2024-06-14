---
title: Testing the Installation
---

To test that the installation was successful we can deploy a workshop. For this
we will use a publicly available workshop by running the command:

```terminal:execute
command: educates deploy-workshop -f https://github.com/vmware-tanzu-labs/lab-k8s-fundamentals/releases/latest/download/workshop.yaml
```

To access the training portal service and browse the workshops hosted by it,
run the command:

```terminal:execute
command: educates browse-workshops
```

When the training portal service is ready, this should automatically open a new
web browser window. Unfortunately though this doesn't work reliably when using
the command inside the terminal of an Educates workshop session due to browser
popup restrictions, it should however work were you running it in a terminal on
your local machine. You can either click one more time, or click or copy the URL
that's been printed in the terminal.