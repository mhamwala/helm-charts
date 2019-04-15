# Knative Build

This chart installs Knative components for Build.
[Knative](https://github.com/knative/) extends Kubernetes to provide a set of middleware components that are essential to build modern, source-centric, and container-based applications that can run anywhere: on premises, in the cloud, or even in a third-party data center.

## Introduction

This is a helm chart for installing Knative build which provides you a standard, portable, reusable, and performance optimized method for defining and running Knative builds on a kubernetes cluster. Visit [knative build](https://github.com/knative/build/blob/master/README.md) for more information.

## Chart Details

In its default configuration, this chart will create the following Kubernetes resources:

- Knative Build:
    - Deployments: controller, webhook
    - Service: controller, webhook
    - ServiceAccount: build-controller

## Prerequisites
- Requires kubectl v1.10+.
- Knative requires a Kubernetes cluster v1.11 or newer with the
[MutatingAdmissionWebhook admission controller](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/#how-do-i-turn-on-an-admission-controller)
enabled.

## Installing the Chart

Please ensure that you have reviewed the [prerequisites](#prerequisites).

1. Install Knative crds
```bash
$ kubectl install -f incubator/knative/all-crds.yaml
```

2. Install the chart using helm cli:

```bash
$ helm install incubator/knative/charts/build --name <my-release> [--tls]
```

The command deploys Knative Build on the Kubernetes cluster in the default configuration.  The [configuration](#configuration) section lists the parameters that can be configured during installation.

You can use the command ```helm status <my-release> [--tls]``` to get a summary of the various Kubernetes artifacts that make up your Knative deployment.

### Configuration

| Parameter                                  | Description                              | Default |
|--------------------------------------------|------------------------------------------|---------|
| `build.enabled`                                  | Enable/Disable Knative Build             | `true`    |
| `build.buildController.image`                    | Build Controller Image                   | gcr.io/knative-releases/github.com/knative/build/cmd/controller@sha256:77b883fec7820bd3219c011796f552f15572a037895fbe7a7c78c7328fd96187    |
| `build.buildController.replicas`                 | Number of pods for Build Contoller       |    1      |
| `build.buildWebhook.image`                       | Build Webhook Image                      | gcr.io/knative-releases/github.com/knative/build/cmd/webhook@sha256:488920f65763374a2886860e3b06c3b614ee685b68ec4fdbbcd08d849bb84b71  |
| `build.buildWebhook.replicas`                    | Number of pods for Build Webhook         |    1      |
| `build.credsInit.image`                          | credsInit Image                          |    gcr.io/knative-releases/github.com/knative/build/cmd/creds-init@sha256:ebf58f848c65c50a7158a155db7e0384c3430221564c4bbaf83e8fbde8f756fe    |
| `build.gcsFetcher.image`                         | gcsFetcher Image                          |    gcr.io/cloud-builders/gcs-fetcher      |
| `build.gitInit.image`                            | gitInit Image                            |    gcr.io/knative-releases/github.com/knative/build/cmd/git-init@sha256:09f22919256ba4f7451e4e595227fb852b0a55e5e1e4694cb7df5ba0ad742b23      |
| `build.nop.image`                                | nop Image                                |    gcr.io/knative-releases/github.com/knative/build/cmd/nop@sha256:a318ee728d516ff732e2861c02ddf86197e52c6288049695781acb7710c841d4      |

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
$ kubectl delete -f incubator/knative/all-crds.yaml
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Limitations

You must use `knative-build` namespace to install Knative build.

## Documentation

Documentation of the Knative build system can be found on the [Knative Build Docs](https://github.com/knative/build/blob/master/README.md).

To learn more about Knative in general, see the [Overview](https://github.com/knative/docs/blob/master/README.md).

# Support

If you're a developer, operator, or contributor trying to use Knative, the
following resources are available for you:

- [Knative Users](https://groups.google.com/forum/#!forum/knative-users)
- [Knative Developers](https://groups.google.com/forum/#!forum/knative-dev)

For contributors to Knative, we also have [Knative Slack](https://slack.knative.dev).
