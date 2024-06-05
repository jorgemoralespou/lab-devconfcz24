---
title: Workshop Definition
---

The publishing lifecycle as described pertains to the workshop files used for
workshop instructions as well as any other files, scripts or applications used
within the workshop session. These will be downloaded for each distinct workshop
session.

When the workshop was deployed using the `educates deploy-workshop` command, the
configuration of the workshop environment was dictated by the workshop
definition. This is a Kubernetes resource which describes where the workshop
files can be found, as well as what capabilities are required for a workshop.

When using the standard workshop directory structure, the workshop definition
can be found in the `resources/workshop.yaml` file.

```editor:open-file
file: ~/lab-demo-workshop/resources/workshop.yaml
```

Actual deployment of a workshop environment based on the workshop definition
only occurs when the workshop is registered with a training portal.

When publishing a workshop, no update is made to the workshop definition
of any workshop environment that has already been created.

When a training portal is configured to monitor for changes to the workshop
definition, updating the workshop definition will trigger the creation of a new
workshop environment based on the new workshop definition and the old workshop
environment will be shutdown, being deleted when all active workshop sessions
against it have completed. Any new requests for the workshop will be directed
towards the new workshop environment.

This is done by first making the required changes to the workshop definition:

```editor:select-matching-text
file: ~/lab-demo-workshop/resources/workshop.yaml
text: 'description: "(.*)"'
isRegex: true
group: 1
```

```editor:replace-text-selection
file: ~/lab-demo-workshop/resources/workshop.yaml
text: "An awesome workshop to demo use of Educates."
```

Because you have a live preview running for the existing version of the
workshop, you will need to exit it.

```terminal:interrupt
```

Next update the workshop definition in the cluster using the command:

```terminal:execute
command: educates update-workshop
```

In your other web browser window terminate the running instance of the workshop
session for the demo workshop. Upon returning to the training portal you should
see that the description of the workshop has now changed.