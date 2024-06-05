---
title: Manually Updating
---

As demonstrated, the basic lifecyle for updating workshop content is to make any
modifications, publish the workshop files as an OCI image to an image registry,
and then create a new workshop session to see any changes.

When making lots of small changes it is possible to short circuit this process
and use one of two mechanisms for making updates in a running workshop session.

The first of these still entails re-publishing the workshop files, but we can
avoid the need to create a new workshop session by manually pulling down the
changes into the current live workshop session. This is done by running the
`update-workshop` command inside of the workshop container.

Make another change to the workshop overview page of the demo workshop.

```editor:append-lines-to-file
file: ~/lab-demo-workshop/workshop/content/00-workshop-overview.md
text: |
  Once you have finished the workshop, I am sure you will agree.
```

Publish the workshop files:

```terminal:execute
command: educates publish-workshop
```

Now jump back to demo workshop in the other web browser window and in the
terminal run:

```workshop:copy
text: update-workshop
```

Reload the workshop instructions pane on the left hand side by holding down the
shift key at the same time as clicking on the reload icon to the right hand side
of the countdown clock in the workshop dashboard. Alternatively right click on
the workshop instructions pane and use the browser menu option to reload the
frame.

Once the workshop instructions have been reloaded, you should see the changes.