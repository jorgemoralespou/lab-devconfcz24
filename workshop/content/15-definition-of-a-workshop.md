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

As the Workshop is another Kubernetes Custom Resource, you can get the details with `kubectl`.

```terminal:execute
command: kubectl get workshops -o yaml
```

**NOTE:** This custom resource does not have a `status` field as it's only the static definition of a workshop


Let's now do some cleanup and create our own Educates workshop.


```terminal:execute
command: educates delete-workshop -f https://github.com/vmware-tanzu-labs/lab-k8s-fundamentals/releases/latest/download/workshop.yaml
cascade: true
```
```terminal:execute
command: educates delete-portal
cascade: true
```
```execute-all
clear
```

**NOTE:** You might have noticed that last command you didn't need to click it, as it 
was configured to automatically execute upon completion of the previous command. Isn't it sweat?