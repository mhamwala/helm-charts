# Natss Provisioner for Knative Eventing

This chart installs Natss Provisioner components for Knative Eventing.
[Knative](https://github.com/knative/) extends Kubernetes to provide a set of middleware components that are essential to build modern, source-centric, and container-based applications that can run anywhere: on premises, in the cloud, or even in a third-party data center.

## Introduction

This chart is a subchart of Knative Eventing. It installs Natss Provisioner. Visit [Eventing](https://github.com/knative/eventing/blob/master/README.md) to find out more about Knative Eventing.

## Chart Details

In its default configuration, this chart will create the following Kubernetes resources:

- Natss Provisioner for Knative Eventing:
    - Deployments: natss-controller, natss-dispatcher, eventing-controller, webhook
    - ServiceAccounts: in-memory-channel-controller, in-memory-channel-dispatcher, eventing-controller, eventing-webhook
    - Service: webhook

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
$ helm install incubator/knative/charts/eventing/charts/natssprovisioner --name <my-release> [--tls]
```

The command deploys Knative Eventing and Natss Provisioner on your Kubernetes cluster in the default configuration.  The [configuration](#configuration) section lists the parameters that can be configured during installation.

You can use the command ```helm status <my-release> [--tls]``` to get a summary of the various Kubernetes artifacts that make up your Knative deployment.

### Configuration

| Parameter                                  | Description                              | Default |
|--------------------------------------------|------------------------------------------|---------|
| `eventing.enabled`                         | Enable/Disable Knative Eventing          | `false`   |
| `eventing.eventingController.image`        | Controller Image                         | gcr.io/knative-releases/github.com/knative/eventing/cmd/controller@sha256:de1727c9969d369f2c3c7d628c7b8c46937315ffaaf9fe3ca242ae2a1965f744 | 
| `eventing.eventingController.replicas`                        | Controller Replicas                      | 1         |
| `eventing.webhook.image`                   | Webhook Image                            | gcr.io/knative-releases/github.com/knative/eventing/cmd/webhook@sha256:3c0f22b9f9bd9608f804c6b3b8cbef9cc8ebc54bb67d966d3e047f377feb4ccb |
| `eventing.webhook.replicas`                | Webhook Replicas                         | 1         |
| `eventing.natssProvisioner.enabled`        | Enable/Disable NATS Provisioner          | `false`   |
| `eventing.natssProvisioner.natssController.controller.image` | Controller Image | gcr.io/knative-releases/github.com/knative/eventing/contrib/natss/pkg/controller@sha256:c0ee52280ba652fa42d6a60ad5e51d7650244043b05e7fd6d693dfbfceb8abd6 |
| `eventing.natssProvisioner.natssController.replicas` | Controller Replicas            | 1         | 
| `eventing.natssProvisioner.natssDispatcher.dispatcher.image` | Dispatcher Image       | gcr.io/knative-releases/github.com/knative/eventing/contrib/natss/pkg/dispatcher@sha256:2de14f9876d0288060bae5266e663f9d77c130a8d491680438552b70cf394ca5 |
| `eventing.natssProvisioner.natssDispatcher.replicas` | Dispatcher Replicas            | 1         |

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

You must use `knative-eventing` namespace to install this chart.

## Documentation

To learn more about Knative in general, see the [Knative Documentation](https://www.knative.dev/docs).

# Support

If you're a developer, operator, or contributor trying to use Knative, the
following resources are available for you:

- [Knative Users](https://groups.google.com/forum/#!forum/knative-users)
- [Knative Developers](https://groups.google.com/forum/#!forum/knative-dev)

For contributors to Knative, we also have [Knative Slack](https://slack.knative.dev).
