---
title: Updating Instructions
---

To update the workshop instructions open up the editor on the workshop overview
page found in the `workshop/content` directory.

```editor:open-file
file: ~/lab-demo-workshop/workshop/content/00-workshop-overview.md
```

Select the paragraph describing the workshop:

```editor:select-matching-text
file: ~/lab-demo-workshop/workshop/content/00-workshop-overview.md
text: "^This is .*$"
isRegex: true
```

and replace it with a better description of this workshop.

```editor:replace-text-selection
file: ~/lab-demo-workshop/workshop/content/00-workshop-overview.md
text: |
  This demo workshop is intended to demonstrate how awesome Educates is.
```

After having made the change re-publish the workshop files so that they will be
picked up for any freshly created workshop sessions.

```terminal:execute
command: educates publish-workshop
```

In the separate web browser window where the demo workshop is running, terminate
the workshop session (see picture below) and create a new workshop session from the training portal.
You should now see the modifications you made.

{{< figure src="../images/workshop-controls.png" >}}

Note that obviously we used the embedded editor provided by the workshop session
to update the workshop files. When working from your own local computer you can
use whatever editor you would normally use.