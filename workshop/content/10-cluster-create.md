---
title: Cluster Installation
---

The name of the Educates CLI is `educates`, and there's flavors of the CLI for 
MacOS and Linux, both AMD64 and ARM64, which can be found in 
[the project's GitHub repository](https://github.com/vmware-tanzu-labs/educates-training-platform/releases)

To install Educates (and associated services) into an existing Kubernetes cluster 
the CLI command which needs to be used is:

```
educates admin platform deploy
```

Before running this command an appropriate configuration file needs to be
created.

For installation of Educates into the virtual cluster created for this workshop
session we will use the following configuration. Click on the action block below
to automatically open the embedded editor and create the file for you.

```editor:append-lines-to-file
file: ~/vcluster-config.yaml
cooldown: .INF
text: |
    # Specify the infrastructure provider hosting the Kubernetes cluster.

    clusterInfrastructure:
        provider: vcluster

    # Specify the ingress domain to be used to access the workshops hosted by
    # the Educates installation.

    clusterIngress:
        domain: {{< param session_name >}}.{{< param ingress_domain >}}

    # Disable the cluster and security policy engines, and skip installing
    # Kyverno, as policies are enforced by the Educates installation running
    # this workshop session.

    clusterPackages:
        kyverno:
            enabled: false

    clusterSecurity:
        policyEngine: none

    workshopSecurity:
        rulesEngine: none        
```

The two key bits of information that we are supplying here are the type of
infrastructure provider and what domain name should be used to access workshops
hosted by the cluster after Educates has been installed.

For this workshop session running in Educates, we set the ingress domain for
our Educates installation to correspond to the ingress domain allocated for
this workshop session.

To make it easier to install Educates into a freshly created Kubernetes cluster
a number of opinionated configurations are provided for different infrastructure
providers, such as EKS (AWS), GKE (GCP) and AKS (Azure). In this case we have
set the provider as `vcluster` corresponding to what would be expected for a
virtual cluster created using the
[vCluster](https://github.com/loft-sh/vcluster) package from [Loft
Labs](https://loft.sh/). 

To see what hidden configuration was added in the case of setting the provider
to `vcluster`, run:

```terminal:execute
command: educates admin platform deploy --config vcluster-config.yaml --show-packages-values --skip-image-resolution
```

The aim of the opinionated cluster configurations is thus to take a fresh
Kubernetes cluster and install everything you need to run Educates, as well as
Educates itself. 

Other configuration we have included above isn't strictly necessary and
everything will work without supplying it, but since we are using Educates to
demonstrate installation of Educates, we don't need to enable the cluster and
workshop security policy engine, nor install Kyverno which is normally used to
implement such policies, as the underlying Educates installation this workshop
session is running in is already enforcing security policies for everything we
are doing. Disabling this will speed up our installation a bit, but for a real
Educates installation you should keep the security policy engines enabled.

Refer to the documentation if you want to learn more about this topic.