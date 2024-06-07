---
title: Definition of a workshop
---

The `Workshop` is a Kubernetes custom resource that defines, amongst other:

- Name and description
- T-shirt size for the associated namespace's resources (Memory and Cpu)
- Security enforcement mechanism
- The location of the content of the workshop
- The capabilities and it's configuration that the workshop will have
  - Console (Terminals)
  - Editor
  - Slides
  - Dashboards
  - Docker
  - Registry
  - ...
- Kubernetes objects definitions that will need to be created along with the session

Read the documentation if you want to know more about the 
[Workshop resource](https://docs.educates.dev/custom-resources/workshop-definition)

As the Workshop is another Kubernetes Custom Resource, you can get the details with `kubectl`.

```terminal:execute
command: kubectl get workshops -o yaml
```

**NOTE:** This custom resource does not have a `status` field as it's only the static definition of a workshop

If you have launched the workshop `Kubernetes Fundamentals` on the other tab in your browser, you might
see some of these capabilities, like the embedded Kubernetes console and slides, along with the terminals and editor
that you can see in this workshop.