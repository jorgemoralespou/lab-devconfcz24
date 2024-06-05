---
title: Cleaning up the environment
---

Let's now do some cleanup before we proceed to create our own Educates workshop.

The following commands will delete the workshop and the training portal that were created
and will clear both terminals.

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