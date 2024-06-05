- [x] On [Cluster Installation](./workshop/content/11-educates-install.md) it fails because KUBECONFIG is not set and it fails to find config in ~/.kube/config
- [x] On [Cluster Installation](./workshop/content/11-educates-install.md) installation fails because:
  ```
  Error: unable to create localhost loopback service: services "loopback" already exists
  ```
  **NOTE**: Maybe the installer does not need to create the loopback for vcluster setup?

- [ ] On [Testing the installation](./workshop/content/12-testing-the-installation.md), the workshop that is deployed does not need an access
  code if the used did click on the popup blocker and access with the code already.
- [ ] On [Definition of a workshop](./workshop/content/15-definition-of-a-workshop.md), the workshop is not deleted at the end with that command.
- [ ] Realtime updates on [Realtime updates](./workshop/content/25-realtime-updates.md) is not working. Maybe because I'm also doing realtime updates on the host workshop and it seems that it might redirect the services to the host?