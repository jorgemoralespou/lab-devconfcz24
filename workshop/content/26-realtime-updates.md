---
title: Realtime Updates
---

The second option for updating workshop content within the running workshop
session involves a bit more magic.

To demonstrate this mechanism run the command:

```terminal:execute
command: educates serve-workshop --patch-workshop
```

It is normal that this command doesn't return. You should be good to go as long
as it says:

```
Proxy listening on: 0.0.0.0:10081
```

Exit the running instance of the demo workshop you have running in your other
web browser window and start a new workshop session. Confirm you can see the
same workshop instructions you had previously.

**NOTE:** Do not proceed with next step until you have gotten a new session 
on your test workshop (with live updates enabled).

Make some more changes to the workshop instructions.

```editor:append-lines-to-file
file: ~/lab-demo-workshop/workshop/content/00-workshop-overview.md
text: |

  Especially when you see the live update feature in action.
```

This time we will not re-publish the workshop content. Instead, immediately swap
back to the other web browser window running the demo workshop. You should see
that it has already been updated with the changes.

The manner by which this works was that the existing deployed workshop was
patched on the fly to get the workshop instructions from the local process
created when you ran the `educates serve-workshop` command.

More specifically, since the rendering of workshop instructions is done using
the [Hugo](https://gohugo.io/) static site renderer, we ran the Hugo live
renderer, with the workshop session dashboard displaying the live view from the
local Hugo process. When changes are made to the local workshop files, Hugo will
automatically detect this and the view displayed in the workshop session
dashboard would be updated. You are thus able to quickly make changes without
needing to re-publish the workshop, or create a new workshop session.
