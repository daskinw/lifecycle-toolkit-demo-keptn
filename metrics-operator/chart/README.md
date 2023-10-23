# Keptn Metrics Operator

Keptn Metrics Operator introduces a more cloud-native approach for handling all metrics related to your application and
infrastructure.
It represents metrics in a uniform format, facilitating the re-usability of this data across multiple components
and allowing the usage of multiple observability platforms.
You can write SLO and SLI based on multiple data coming from multiple sources such as:
Prometheus, Dynatrace, DataDog and K8s metric server...

<!-- markdownlint-disable MD012 -->

## Parameters

### Keptn Metrics Operator common

| Name                                   | Description                                                                                                                                                   | Value               |
| -------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------- |
| `replicas`                             | customize number of installed metrics operator replicas                                                                                                       | `1`                 |
| `operatorService.ports[0]`             | webhook port (must correspond to Mutating Webhook Configurations)                                                                                             |                     |
| `operatorService.ports[0].name`        |                                                                                                                                                               | `https`             |
| `operatorService.ports[0].port`        |                                                                                                                                                               | `8443`              |
| `operatorService.ports[0].protocol`    |                                                                                                                                                               | `TCP`               |
| `operatorService.ports[0].targetPort`  |                                                                                                                                                               | `https`             |
| `operatorService.ports[1]`             | port to integrate with the K8s custom metrics API                                                                                                             |                     |
| `operatorService.ports[1].name`        |                                                                                                                                                               | `custom-metrics`    |
| `operatorService.ports[1].port`        |                                                                                                                                                               | `443`               |
| `operatorService.ports[1].targetPort`  |                                                                                                                                                               | `custom-metrics`    |
| `operatorService.ports[2]`             | port to integrate with metrics API (e.g. Keda)                                                                                                                |                     |
| `operatorService.ports[2].name`        |                                                                                                                                                               | `metrics`           |
| `operatorService.ports[2].port`        |                                                                                                                                                               | `9999`              |
| `operatorService.ports[2].protocol`    |                                                                                                                                                               | `TCP`               |
| `operatorService.ports[2].targetPort`  |                                                                                                                                                               | `metrics`           |
| `operatorService.type`                 |                                                                                                                                                               | `ClusterIP`         |
| `config.health.healthProbeBindAddress` | setup on what address to start the default health handler                                                                                                     | `:8081`             |
| `config.leaderElection.leaderElect`    | decides whether to enable leader election with multiple replicas                                                                                              | `true`              |
| `config.leaderElection.resourceName`   | defines LeaderElectionID                                                                                                                                      | `3f8532ca.keptn.sh` |
| `config.metrics.bindAddress`           | MetricsBindAddress is the TCP address that the controller should bind to for serving prometheus metrics. It can be set to "0" to disable the metrics serving. | `127.0.0.1:8080`    |
| `config.webhook.port`                  |                                                                                                                                                               | `9443`              |
| `Mutating`                             | Webhook Configurations for metrics Operator                                                                                                                   |                     |
| `webhookService.ports[0].port`         |                                                                                                                                                               | `443`               |
| `webhookService.ports[0].protocol`     |                                                                                                                                                               | `TCP`               |
| `webhookService.ports[0].targetPort`   |                                                                                                                                                               | `9443`              |
| `webhookService.type`                  |                                                                                                                                                               | `ClusterIP`         |
| `nodeSelector`                         | add custom nodes selector to metrics operator                                                                                                                 | `{}`                |
| `tolerations`                          | add custom tolerations to metrics operator                                                                                                                    | `[]`                |
| `topologySpreadConstraints`            | add custom topology constraints to metrics operator                                                                                                           | `[]`                |

### Keptn Metrics Operator controller

| Name                                                | Description                                       | Value                            |
| --------------------------------------------------- | ------------------------------------------------- | -------------------------------- |
| `containerSecurityContext`                          | Sets security context privileges                  |                                  |
| `containerSecurityContext.allowPrivilegeEscalation` |                                                   | `false`                          |
| `containerSecurityContext.capabilities.drop`        |                                                   | `["ALL"]`                        |
| `containerSecurityContext.privileged`               |                                                   | `false`                          |
| `containerSecurityContext.runAsGroup`               |                                                   | `65532`                          |
| `containerSecurityContext.runAsNonRoot`             |                                                   | `true`                           |
| `containerSecurityContext.runAsUser`                |                                                   | `65532`                          |
| `containerSecurityContext.seccompProfile.type`      |                                                   | `RuntimeDefault`                 |
| `image.repository`                                  | specify registry for manager image                | `ghcr.io/keptn/metrics-operator` |
| `image.tag`                                         | select tag for manager image                      | `v0.8.2`                         |
| `env.exposeKeptnMetrics`                            | enable metrics exporter                           | `true`                           |
| `env.metricsControllerLogLevel`                     | sets the log level of Metrics Controller          | `0`                              |
| `env.analysisControllerLogLevel`                    | sets the log level of Analysis Controller         | `0`                              |
| `env.enableKeptnAnalysis`                           | enables/disables the analysis feature             | `false`                          |
| `livenessProbe`                                     | custom livenessprobe for manager container        |                                  |
| `readinessProbe`                                    | custom readinessprobe for manager container       |                                  |
| `resources`                                         | specify limits and requests for manager container |                                  |

### Global

| Name                      | Description                            | Value           |
| ------------------------- | -------------------------------------- | --------------- |
| `kubernetesClusterDomain` | overrides domain.local                 | `cluster.local` |
| `imagePullSecrets`        | global value for image registry secret | `[]`            |