# Demo Workshop for DevConf CZ 24

Workshop to demo use of Educates.

If you want to run this workshop yourself, on your local machine, you just need
to follow this simple steps:

1. Download [educates 3.x CLI](https://github.com/vmware-tanzu-labs/educates-training-platform/releases) for your OS architecture
2. [Create your local educates cluster (with the provided config file)](#create-a-local-cluster-for-deployment-of-workshop-or-develop)
3. [Publish and deploy the workshop](#publish-and-deploy-workshop)
4. [Access the workshop](#access-the-workshop)

## Create a local cluster (for deployment of workshop or develop)
In order to run this workshop you will need `kapp-controller` installed. The easiest way to have a local
development cluster with kapp-controller is by using the `educates` CLI and enable `kapp-controller` package:

Create a config file: (e.g. `kind-config.yaml`). [We already provide a working sample
config file](./kind-config.yaml):

```
clusterPackages:
  kapp-controller:
    enabled: true
```

And create an educates local cluster:

```
educates admin cluster create --config=kind-config.yaml
```

## Publish and deploy workshop

Once you have the cluster up and running, it's time to build a local instance of the workshop:

```
educates publish-workshop
```

And then, deploy this to the cluster:

```
educates deploy-workshop
```

## Access the workshop

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

## Develop content locally

If you want to develop static content locally, you can run Hugo from within your host and forward it to the workshop session
running on educates.

```
educates serve-workshop --patch-workshop
```

See [docs](https://docs.educates.dev/workshop-content/working-on-content#working-on-content)
