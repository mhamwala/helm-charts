# Knative Eventing Sources

This chart installs Knative components for Eventing Sources.
[Knative](https://github.com/knative/) extends Kubernetes to provide a set of middleware components that are essential to build modern, source-centric, and container-based applications that can run anywhere: on premises, in the cloud, or even in a third-party data center.

## Introduction

This is a helm chart for installing Knative Eventing Sources which provides loosely coupled services that can be developed and deployed on independently on Kubernetes. Visit [knative eventing sources](https://github.com/knative/eventing-sources/blob/master/README.md) for more information.

## Chart Details

In its default configuration, this chart will create the following Kubernetes resources:

- Knative Eventing Sources:
    - StatefulSet: controller-manager
    - ServiceAccount: controller-manager
    - Service: controller

## Prerequisites
- Requires kubectl v1.10+.
- Knative requires a Kubernetes cluster v1.11 or newer with the
[MutatingAdmissionWebhook admission controller](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/#how-do-i-turn-on-an-admission-controller)
enabled.
- Istio - You should have Istio installed on your Kubernetes cluster. If you do not have it installed already you can do so by running the following commands:
```bash
$ kubectl apply --filename https://github.com/knative/serving/releases/download/v0.5.0/istio-crds.yaml 
$ kubectl apply --filename https://github.com/knative/serving/releases/download/v0.5.0/istio.yaml
```
or by following these steps:
[Installing Istio](https://www.knative.dev/docs/install/knative-with-any-k8s/#installing-istio)

## Installing the Chart

Please ensure that you have reviewed the [prerequisites](#prerequisites).

1. Install Knative crds
```bash
$ kubectl install -f incubator/knative/all-crds.yaml
```

2. Install the chart using helm cli:

```bash
$ helm install incubator/knative/charts/eventingsources --name <my-release> [--tls]
```

The command deploys Knative Eventing Sources on your Kubernetes cluster in the default configuration.  The [configuration](#configuration) section lists the parameters that can be configured during installation.

You can use the command ```helm status <my-release> [--tls]``` to get a summary of the various Kubernetes artifacts that make up your Knative deployment.

### Configuration

| Parameter                                  | Description                              | Default |
|--------------------------------------------|------------------------------------------|---------|
| `eventingSources.enabled`                  | Enable/Disable Knative Eventing Sources  | `false`   |
| `eventingSources.controllerManager.manager.image`        | Manager Image for Controller Manager | gcr.io/knative-releases/github.com/knative/eventing-sources/cmd/manager@sha256:deb40ead1bd4eedda8384d1e6d535cf75f1820ac723fdaa0c4670636ca94cf2e   |
| `eventingSources.camel.enabled`            | Enable/Disable Apache Camel Event Source | `false`   |
| `eventingSources.camel.camelControllerManager.manager.image`        | Manager Image for Camel Controller Manager | gcr.io/knative-releases/github.com/knative/eventing-sources/contrib/camel/cmd/controller@sha256:1c4631019f85cf63b7d6362a99483fbaae65277a68ac004de15168a79e90be73   |
| `eventingSources.eventDisplay.enabled`     | Enable/Disable A Knative Service that logs events received for use in samples and debugging. | `false`   |
| `eventingSources.eventDisplay.eventDisplay.image`        | Event Display Image for Event Display | gcr.io/knative-releases/github.com/knative/eventing-sources/cmd/event_display@sha256:bf45b3eb1e7fc4cb63d6a5a6416cf696295484a7662e0cf9ccdf5c080542c21d   |
| `eventingSources.gcpPubSub.enabled`        | Enable/Disable GCP Event Source          | `false`   |
| `eventingSources.gcpPubSub.gcppubsubControllerManager.manager.image`        | Google Cloud Platform Pub Sub Controller Manager Image | gcr.io/knative-releases/github.com/knative/eventing-sources/contrib/gcppubsub/cmd/controller@sha256:cde83a9f10c3c1340c93a9a9fd5ba76c9f7c33196fdab98a4c525f9cd5d3bb1f   |

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`.

### Verifying the Chart

To verify all Pods are running, try:
```bash
$ helm status <my-release> [--tls]
```

## Uninstalling the Chart

To uninstall/delete the deployment:
```bash
$ helm delete <my-release> --purge [--tls]
```

To uninstall/delete the crds:
```bash
$ kubectl delete -f knative/all-crds.yaml
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Limitations

You must use `knative-sources` namespace to install Knative Eventing Sources.

## Documentation

Documentation of the Knative eventing system can be found on the [Knative Eventing Sources Docs](https://github.com/knative/eventing-sources/blob/master/README.md).

To learn more about Knative in general, see the [Overview](https://github.com/knative/docs/blob/master/README.md).

# Support

If you're a developer, operator, or contributor trying to use Knative, the
following resources are available for you:

- [Knative Users](https://groups.google.com/forum/#!forum/knative-users)
- [Knative Developers](https://groups.google.com/forum/#!forum/knative-dev)

For contributors to Knative, we also have [Knative Slack](https://slack.knative.dev).
