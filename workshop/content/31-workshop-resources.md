---
title: Workshop Resources
---

Sometimes you need your workshop session to have things already existing for the 
user to be able to exercise your workshop. Educates allows you to deploy additional
Kubernetes resources along with your session, or shared for all workshop sessions. 
This option can be handy when you want all attendees to share access to a single resource,
or when a resource can only be created once in a shared cluster (e.g. CRDs) or even to
save on cluster resources.

Let's see how you can deploy a simple hello-world application and expose it in 
the workshop tabs.

```editor:open-file
file: ~/lab-demo-workshop/resources/workshop.yaml
```

```editor:select-matching-text
file: ~/lab-demo-workshop/resources/workshop.yaml
text: "console:"
after: 1
```
  
```editor:replace-text-selection
file: ~/lab-demo-workshop/resources/workshop.yaml
text: |2
        console:
          enabled: true
```

```editor:insert-value-into-yaml
file: ~/lab-demo-workshop/resources/workshop.yaml
path: spec.session
value:
  objects:
  - apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: webapp
    spec:
      replicas: 1
      selector:
        matchLabels:
          deployment: webapp
      strategy:
        type: Recreate
      template:
        metadata:
          labels:
            deployment: webapp
        spec:
          containers:
          - name: webapp
            image: ghcr.io/jorgemoralespou/lab-devconfcz24-webapp:latest
            imagePullPolicy: IfNotPresent
            ports:
            - containerPort: 8080
              protocol: TCP
  - apiVersion: v1
    kind: Service
    metadata:
      name: webapp
    spec:
      type: ClusterIP
      ports:
      - port: 8080
        targetPort: 8080
      selector:
        deployment: webapp
```
BLABLABLA

This is done by first making the required changes to the workshop definition:

```editor:insert-value-into-yaml
file: ~/lab-demo-workshop/resources/workshop.yaml
path: spec.session
value:
  ingresses:
  - name: webapp
    protocol: http
    port: 8080
    host: webapp.$(session_namespace).svc.$(cluster_domain)
  dashboards:
  - name: Webapp
    url: $(ingress_protocol)://webapp-$(session_hostname)
```

This will be accesible at `{{< param ingress_protocol >}}://webapp-{{< param session_hostname >}}`

Next update the workshop definition in the cluster using the command:

```terminal:execute
command: educates update-workshop
```

~~~editor:append-lines-to-file
file: ~/lab-demo-workshop/workshop/content/00-workshop-overview.md
text: |

  ```dashboard:open-dashboard
  name: Webapp
  ```

  ```dashboard:open-dashboard
  name: Console
  ```
~~~

```terminal:execute
command: educates publish-workshop
```
