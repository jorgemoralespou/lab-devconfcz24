---
title: The training portal
---

The `Training Portal`, effectively is a Kubernetes `Custom Resource`, so one can use Kubernetes client
to get details about the resource:

```terminal:execute
command: kubectl get trainingportal
```

Or the full yaml with all the configuration it contains:

```terminal:execute
session: 2
command: kubectl get trainingportal educates-cli -o yaml
```

The trainingportal defines runtime configuration for each workshop it exposes, like
maximum number of sessions, duration for the workshop, idle time to be considered abandoned, 
and many more as well as the url and credentials to access the portal in different ways.

Read the documentation if you want to know more about the 
[TrainingPortal resource](https://docs.educates.dev/custom-resources/training-portal)

