# Kustomize and Terraform for the win.
__not yet implemented__

Kustomize helps us maintain the difference between environment specs in a simple manner through templating.
But if you're running kubectl to do shit, you're doing it wrong. (like, at work anyway so why not build this out the right way?)
IAC is not just yaml files. CI/CD is a key component and we can automate tasks based on events in the k8s controller loop.

[This TF provider](https://registry.terraform.io/providers/kbst/kustomization/latest/docs) solves some major problems with using kustomize alone:
1. lack of a feedback loop with `kubectl apply -k ...` - source: my experience IDK where I read about it years ago?
2. `terraform plan` which you can't do with kustomize
3. you can purge deleted resources
4. Changes to immutable fields will generate a destroy and recreate plan.

- source for 2-4: the link above


## Rocketchat
Okay, so according to [the docs](https://docs.rocket.chat/installing-and-updating/docker-containers) docker is the most widely tested way of running rocketchat. Cool, but who wants pet servers? Gross. Needs some sort of state store to maintain a common state store among replicas in the cluster. Mongo is their DB of choice, I like mongo. Cool. So we need mongo as well as rocket.chat. Do we run databases in prod k8s clusters, no. In this example I will, but only to help keep my own personal cloud bill down. In the real world I would choose a managed service from the cloud provider to fulfil this role. A few other prod considerations: SSL certs, domain mapping, dns automation, secrets, etc...

