# Tekton Pipelines

This chart installs Tekton Pipelines.

## Introduction

- Visit [Tekton Pipelines](https://github.com/tektoncd/pipeline/blob/master/README.md) for more information.

## Chart Details

In its default configuration, this chart will create the following Kubernetes resources:

- Tekton Piplines:
    - Deployments: tekton-pipelines-controller, tekton-pipelines-webhook
    - Service: tekton-pipelines-controller, tekton-pipelines-webhook
    - ServiceAccount: tekton-pipelines-controller

## Prerequisites

- Requires a Kubernetes cluster v1.12 or newer

## Installing the Chart

Please ensure that you have reviewed the [prerequisites](#prerequisites).

1. Install the chart using helm cli:

```bash
$ helm repo add incubator http://storage.googleapis.com/kubernetes-charts-incubator
$ helm install incubator/tekton-pipelines --name <my-release> [--tls]
```

The command deploys tekton-pipelines on the Kubernetes cluster in the default configuration.  The [configuration](#configuration) section lists the parameters that can be configured during installation.

You can use the command ```helm status <my-release> [--tls]``` to get a summary of the various Kubernetes artifacts that make up your tekton-pipelines deployment.

### Configuration

| Parameter                                  | Description                              | Default |
|--------------------------------------------|------------------------------------------|---------|
| `tektonPipelinesController.image`                    | Tekton Pipelines Controller Image                   | gcr.io/tekton-releases/github.com/tektoncd/pipeline/cmd/controller@sha256:e9128c33f5ee55c9d7fcafc914487a23dd0348e45bf14e644d71f8b73dae9061    |
| `tektonPipelinesController.replicas`                 | Number of pods for Tekton Pipelines Contoller       |    1      |
| `tektonPipelinesWebhook.replicas`                    | Number of pods for Tekton Pipelines Webhook         |    1      |
| `tektonPipelinesWebhook.webhook.image`                       | Tekton Pipelines Webhook Image                      | gcr.io/tekton-releases/github.com/tektoncd/pipeline/cmd/webhook@sha256:9842623ed07f6efc0dac227dab263e295f7ddc48ab029b20a7ee0ec1e66b0c4a  |

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

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Limitations

Look inside each subchart to view the their limitations.

## Documentation

To learn more about Tekton in general, see the [Tekton Documentation](https://github.com/tektoncd/pipeline/tree/master/docs).

# Support

If you're a developer, operator, or contributor trying to use Tekton Pipelines, the
following resources are available for you:

- [Tekton/Knative Users](https://groups.google.com/forum/#!forum/knative-users)
- [Tekton Developers](https://github.com/tektoncd/pipeline/tree/master/docs/developers)

For contributors to tekton-pipelines, we also have [Tekton Slack](https://tektoncd.slack.com).
