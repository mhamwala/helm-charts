# Elasticsearch logging for Knative Monitoring

This chart installs Elasticsearch logging components for Knative Monitoring.
[Knative](https://github.com/knative/) extends Kubernetes to provide a set of middleware components that are essential to build modern, source-centric, and container-based applications that can run anywhere: on premises, in the cloud, or even in a third-party data center.

## Introduction

This chart is a subchart of Knative Monitoring. It installs Elasticsearch logging. Visit [accessing logs](https://github.com/knative/docs/blob/master/serving/accessing-logs.md) to find out more.

## Chart Details

In its default configuration, this chart will create the following Kubernetes resources:

- Elasticsearch logging for Knative Monitoring:
    - Deployments: kibana-logging, activator, autoscaler, controller, webhook
    - Service: elasticsearch-logging, fluentd-ds, kibana-logging, activator-service, autoscaler, controller, webhook
    - StatefulSet: elasticsearch-logging, fluentd-ds
    - Gateway: cluster-local-gateway, knative-ingress-gateway
    - ServiceAccount: elasticsearch-logging, fluentd-ds, controller

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
$ helm install incubator/knative/charts/serving/charts/elasticsearch --name <my-release> [--tls]
```

The command deploys Knative Serving, Monitoring and Elastic Search Logging on your Kubernetes cluster in the default configuration.  The [configuration](#configuration) section lists the parameters that can be configured during installation.

You can use the command ```helm status <my-release> [--tls]``` to get a summary of the various Kubernetes artifacts that make up your Knative deployment.

### Configuration

| Parameter                                  | Description                              | Default |
|--------------------------------------------|------------------------------------------|---------|
| `serving.enabled`                          | Enable/Disable Knative Serving           | `true`    |
| `serving.activator.image`                  | Activator Image                          | gcr.io/knative-releases/github.com/knative/serving/cmd/activator@sha256:60630ac88d8cb67debd1e2ab1ecd6ec3ff6cbab2336dda8e7ae1c01ebead76c0   |
| `serving.activatorService.type`            | Activator Ingress Type                   | ClusterIP |
| `serving.autoscaler.image`                 | Autoscaler Image                         | gcr.io/knative-releases/github.com/knative/serving/cmd/autoscaler@sha256:442f99e3a55653b19137b44c1d00f681b594d322cb39c1297820eb717e2134ba   |
| `serving.autoscaler.replicas`              | Autoscaler Replicas                      | 1         |
| `serving.controller.image`                 | Controller Image                         | gcr.io/knative-releases/github.com/knative/serving/cmd/controller@sha256:25af5f3adad8b65db3126e0d6e90aa36835c124c24d9d72ffbdd7ee739a7f571  |
| `serving.controller.replicas`              | Controller Replicas                      | 1         |
| `serving.queueProxy.image`                 | Queue Proxy Image                        | gcr.io/knative-releases/github.com/knative/serving/cmd/queue@sha256:b5c759e4ea6f36ae4498c1ec794653920345b9ad7492731fb1d6087e3b95dc43  |
| `serving.webhook.image`                    | Webhook Image                            | gcr.io/knative-releases/github.com/knative/serving/cmd/webhook@sha256:d1ba3e2c0d739084ff508629db001619cea9cc8780685e85dd910363774eaef6  |
| `serving.webhook.replicas`                 | Webhook Replicas                         | 1         |
| `serving.monitoring.enabled`               | Enable/Disable Knative Monitoring        | `true`    |
| `serving.monitoring.elasticsearch.enabled` | Enable/Disable Elasticsearch Logging     | `true`    |
| `serving.monitoring.elasticsearch.elasticsearchLogging.elasticsearchLoggingInit.image` | Elasticsearch Logging Init Image | alpine:3.6 |
| `serving.monitoring.elasticsearch.elasticsearchLogging.image`   | Elasticsearch Image | k8s.gcr.io/elasticsearch:v5.6.4  |
| `serving.monitoring.elasticsearch.elasticsearchLogging.replicas` | Elasticsearch Replicas | 2     |
| `serving.monitoring.elasticsearch.fluentdDs.image` | Fluentd Image                    | k8s.gcr.io/fluentd-elasticsearch:v2.0.4 |
| `serving.monitoring.elasticsearch.kibanaLogging.image` | Kibana Image                 | docker.elastic.co/kibana/kibana:5.6.4 |
| `serving.monitoring.elasticsearch.kibanaLogging.replicas` | Kibana Replicas           | 1         |
| `serving.monitoring.elasticsearch.kibanaLogging.type` | Kibana Ingress Type           | NodePort  |

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

You must use `knative-monitoring` namespace to install this chart.

## Documentation

To learn more about Knative in general, see the [Knative Documentation](https://www.knative.dev/docs).

# Support

If you're a developer, operator, or contributor trying to use Knative, the
following resources are available for you:

- [Knative Users](https://groups.google.com/forum/#!forum/knative-users)
- [Knative Developers](https://groups.google.com/forum/#!forum/knative-dev)

For contributors to Knative, we also have [Knative Slack](https://slack.knative.dev).
