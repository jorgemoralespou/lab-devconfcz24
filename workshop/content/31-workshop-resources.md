---
title: Workshop Resources
---

Sometimes you need your workshop session to have additional applications
pre-deployed for the user to be able to undertake your workshop. Educates allows
you to deploy additional Kubernetes resources along with your session, or shared
across all workshop sessions. In the case of the latter, the option can be handy
when you want all attendees to share access to a single resource, or when a
resource can only be created once in a shared cluster (e.g. CRDs) or even to
save compute resources on cluster's compute resources.

Let's see how you can deploy a simple hello-world application and expose it in 
the workshop tabs, all ready for your user.

Open up the workshop definition in the editor.

```editor:open-file
file: ~/lab-demo-workshop/resources/workshop.yaml
```

Insert into to the workshop definition a list of Kubernetes resources to be
created with the session.

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

We could have used a Kubernetes ingress to expose the web application publicly,
but in this case we will configure the workshop session to act as a proxy for
accessing the web application. By using the session as proxy, access will be
restricted to just the workshop user.

```editor:insert-value-into-yaml
file: ~/lab-demo-workshop/resources/workshop.yaml
path: spec.session
value:
  ingresses:
  - name: webapp
    protocol: http
    port: 8080
    host: webapp.$(session_namespace).svc.$(cluster_domain)
```

The web application will be accesible at `{{< param ingress_protocol >}}://webapp-{{< param session_hostname >}}`.

At the same time, we integrate access to the web application into the workshop
session dashboard itself as another tab.

```editor:insert-value-into-yaml
file: ~/lab-demo-workshop/resources/workshop.yaml
path: spec.session
value:
  dashboards:
  - name: Webapp
    url: $(ingress_protocol)://webapp-$(session_hostname)
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

Next update the workshop definition in the cluster using the command:

```terminal:execute
command: educates update-workshop
```

We will also add two clickable actions to the workshop we're creating 
to demonstrate how we can open the new tabs we have just added:

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

We update the workshop content by publishing it:
```terminal:execute
command: educates publish-workshop
```

And now, we can navigate to the other browser terminal tab and create
a new instance of the workshop to explore the new features we
just added.