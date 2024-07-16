# Namespaces

## Introduction

A namespace it is like a linux user, every kubernetes object can be ran by a namespace, even every object can appear on more than 1 namespace. This can be use to apply policies at a ns level or manage resources.

It is possible to change context and everything you do from there would be in the name of the ns context.
For example to run a ns context:

```
kubectl config use-context testing

```
Once done, all of our commands will be automatically executed in the testing namespace.

"testing" is the namespace I have created before using the following command:
```
kubectl create namespace testing

```

To delete all the resources of a namespace, run the following command:

```
kubectl delete ns testing

```
