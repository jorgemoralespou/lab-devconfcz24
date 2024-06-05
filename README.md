# Demo Workshop for DevConf CZ 24

Workshop to demo use of Educates.

## Create a local cluster (for deployment of workshop or develop)
In order to run this workshop you will need `kapp-controller` installed. The easiest way to have a local
development cluster with kapp-controller is by using the `educates` CLI and enable `kapp-controller` package:

Create a config file: (e.g. `kind-config.yaml`):

```
clusterPackages:
  kapp-controller:
    enabled: true
```

And create an educates local cluster:

```
educates admin cluster create --config=kind-config.yaml
```

## Deploy workshop

Once you have the cluster up and running, it's time to build a local instance of the workshop:

```
educates publish-workshop
```

And then, deploy this to the cluster:

```
educates deploy-workshop
```

You can now access the workshop by:

```
educates browse-workshops
```

This will automatically access the training portal with the access token. You can also use plain kubectl to find the
details (ingress and portalpassword) to access the training portal:

```
kubectl get trainingportal
```

See [docs](https://docs.educates.dev/workshop-content/working-on-content#working-on-content)

## Develop content locally

If you want to develop static content locally, you can run Hugo from within your host and forward it to the workshop session
running on educates.

```
educates serve-workshop --patch-workshop
```

See [docs](https://docs.educates.dev/workshop-content/working-on-content#working-on-content)
