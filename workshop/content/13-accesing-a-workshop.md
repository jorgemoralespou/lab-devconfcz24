---
title: Accessing Workshops
---

The `training portal` service in Educates provides a gateway for accessing one or
more workshops deployed to the Kubernetes cluster. If required, you can have
more than one training portal service, with each providing access to a different
set of workshops.

{{< figure src="../images/training-portal-ui.png" >}}

The training portal service can be configured to require simple authentication
or access can be anonymous. The user interface provided by the training portal
is designed to be basic and was originally intended to provide a quick way to
provide access to a set of workshops for ad-hoc training, or use in conference
booths for workshops or demos.

If you need a more rich user interface the training portal can be used in a
headless mode, with access to creation of workshops being performed via a REST
API. In this way you can integrate hosting of workshops into your own custom
front end portal or even an existing web site, with user access controlled by
your own SSO system. An example of this is [Spring.academy](https://spring.academy)
site, which offers an integrated experience.

{{< figure src="../images/spring-academy.png" >}}

And fully themed workshops via Educates.

{{< figure src="../images/spring-academy-workshop.png" >}}