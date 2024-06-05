---
title: Structure of a Workshop
---

The workshop template when used creates the following files in the top level directory:

* `README.md` - A file telling everyone what the workshop is about. Replace the current content provided in the sample workshop with your own.

Key sub directories and the files contained within them are:

* `workshop` - Directory under which your workshop files reside.
* `workshop/content` - Directory under which your workshop instructions resides. The files here follow Hugo content rules.
* `resources` - Directory under which Kubernetes custom resources are stored for deploying the workshop using Educates.
* `resources/workshop.yaml` - The custom resource for Educates which describes your workshop and requirements it may have when being deployed.
* `workshop/config.yaml` - Configuration file with details of available modules which make up your workshop, data variables for use in content, and selectable paths through the workshop instructions. This file is optional unless you're going to create Pathways, which is a way to control complex workshops with multiple possible paths. If this file doesn't exist or no configuration is included within it, workshop instructions page ordering will be based on file name sort order, or page weights if defined in the meta data of pages.

If your workshop instructions use images, you should follow the Hugo convention and place images in the `workshop/static` directory, or use page bundles and include the image for a page in the directory for the page bundle.

A workshop may consist of other configuration files, and directories with other types of content, but this is the minimal set of files to get you started.

## Root directory for exercises

Because of possible proliferation of files and directories at the top level of the repository and thus potentially the home directory for the user when running the workshop environment, you can place files required for exercises during the workshop into the `exercises` sub directory below the root of the repository.

When such an `exercises` sub directory exists, the initial working directory for the embedded terminal when created will be set to be `$HOME/exercises` instead of `$HOME`. Further, if the embedded editor is enabled, the sub directory will be opened as the workspace for the editor and only directories and files in that sub directory will be visible through the default view of the editor.

