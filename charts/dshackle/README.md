
# dshackle

![Version: 0.1.12](https://img.shields.io/badge/Version-0.1.12-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square)

Emerald Dshackle is a Fault Tolerant Load Balancer for Blockchain API. Support for standard Bitcoin and Ethereum JSON RPC API over HTTP and WebSocket.

**Homepage:** <https://github.com/emeraldpay/dshackle>

## Source Code

* <https://github.com/emeraldpay/dshackle>
* <https://github.com/drpcorg/dshackle>

## Requirements

| Repository | Name | Version |
|------------|------|---------|
| https://charts.bitnami.com/bitnami | redis | 20.x.x |

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` | Affinity configuration for pods |
| annotations | object | `{}` | Annotations for the StatefulSet |
| autoscaling | object | `{}` | Autoscaling configs for dshackle |
| config | object | See `values.yaml` | Config file |
| containerSecurityContext | object | See `values.yaml` | The security context for containers |
| customArgs | list | `[]` | Custom args for the dshackle container |
| customCommand | list | `[]` | Command replacement for the dshackle container |
| externalHttpPort | int | See `values.yaml` | External HTTP Port, where the service is exposed |
| extraContainers | list | `[]` | Additional containers |
| extraEnv | list | `[]` | Additional env variables |
| extraPorts | list | `[]` | Additional ports. Useful when using extraContainers |
| extraVolumeMounts | list | `[]` | Additional volume mounts |
| extraVolumes | list | `[]` | Additional volumes |
| fullnameOverride | string | `""` | Overrides the chart's computed fullname |
| gRPCPort | int | See `values.yaml` | gRPC Port |
| healthPort | int | See `values.yaml` | Health Port |
| image.pullPolicy | string | `"IfNotPresent"` | dshackle container pull policy |
| image.repository | string | `"emeraldpay/dshackle"` | dshackle container image repository |
| image.tag | string | `"0.15.0"` | dshackle container image tag |
| imagePullSecrets | list | `[]` | Image pull secrets for Docker images |
| ingress.annotations | object | `{}` | Annotations for Ingress |
| ingress.enabled | bool | `false` | Ingress resource for the HTTP API |
| ingress.hosts | list | `[{"host":"chart-example.local","paths":[]}]` | Ingress host |
| ingress.tls | list | `[]` | Ingress TLS |
| initContainers | list | `[]` | Additional init containers |
| internalHttpPort | int | See `values.yaml` | Internal HTTP Port, where pod and application running in the container are listening |
| livenessProbe | object | See `values.yaml` | Liveness probe |
| metricsPort | int | See `values.yaml` | Metrics Port |
| nameOverride | string | `""` | Overrides the chart's name |
| nodeSelector | object | `{}` | Node selector for pods |
| podAnnotations | object | `{}` | Pod annotations |
| podDisruptionBudget | object | `{}` | Define the PodDisruptionBudget spec If not set then a PodDisruptionBudget will not be created |
| podLabels | object | `{}` | Pod labels |
| podManagementPolicy | string | `"OrderedReady"` | Pod management policy |
| priorityClassName | string | `nil` | Pod priority class |
| readinessProbe | object | See `values.yaml` | Readiness probe |
| redis.auth.password | string | `"yourRedisSecret"` |  |
| redis.enabled | bool | `true` | If enabled a redis chart will be deployed as a dependency |
| redis.image.pullPolicy | string | `"IfNotPresent"` |  |
| redis.image.registry | string | `"docker.io"` |  |
| redis.image.repository | string | `"bitnami/redis"` |  |
| redis.image.tag | string | `"7.4.3-debian-12-r0"` |  |
| redis.master.persistence.enabled | bool | `true` |  |
| redis.master.persistence.size | string | `"8Gi"` |  |
| redis.replica.persistence.enabled | bool | `false` |  |
| redis.replica.persistence.size | string | `"8Gi"` |  |
| redis.replica.replicaCount | int | `0` |  |
| replicas | int | `1` | Number of replicas |
| resources | object | `{}` | Resource requests and limits |
| secretEnv | object | `{"INFURA_USER":"your-infura-secret","REDIS_PASSWORD":"yourRedisSecret"}` | Additional env variables injected via a created secret |
| securityContext | object | See `values.yaml` | The security context for pods |
| service.type | string | `"ClusterIP"` | Service type |
| serviceAccount.annotations | object | `{}` | Annotations to add to the service account |
| serviceAccount.create | bool | `true` | Specifies whether a service account should be created |
| serviceAccount.name | string | `""` | The name of the service account to use. If not set and create is true, a name is generated using the fullname template |
| serviceMonitor.annotations | object | `{}` | Additional ServiceMonitor annotations |
| serviceMonitor.enabled | bool | `false` | If true, a ServiceMonitor CRD is created for a prometheus operator https://github.com/coreos/prometheus-operator |
| serviceMonitor.interval | string | `"1m"` | ServiceMonitor scrape interval |
| serviceMonitor.labels | object | `{}` | Additional ServiceMonitor labels |
| serviceMonitor.namespace | string | `nil` | Alternative namespace for ServiceMonitor |
| serviceMonitor.path | string | `"/metrics"` | Path to scrape |
| serviceMonitor.relabelings | list | `[]` | ServiceMonitor relabelings |
| serviceMonitor.scheme | string | `"http"` | ServiceMonitor scheme |
| serviceMonitor.scrapeTimeout | string | `"30s"` | ServiceMonitor scrape timeout |
| serviceMonitor.tlsConfig | object | `{}` | ServiceMonitor TLS configuration |
| terminationGracePeriodSeconds | int | `30` | How long to wait until the pod is forcefully terminated |
| tolerations | list | `[]` | Tolerations for pods # ref: https://kubernetes.io/docs/concepts/configuration/taint-and-toleration/ |
| topologySpreadConstraints | list | `[]` | Topology Spread Constraints for pods # ref: https://kubernetes.io/docs/concepts/scheduling-eviction/topology-spread-constraints/ |
| updateStrategy | object | `{"type":"RollingUpdate"}` | Update stategy for the Statefulset |
| updateStrategy.type | string | `"RollingUpdate"` | Update stategy type |

# Examples

## Connecting to an external Redis instance

```yaml
# Disable the redis deployment
redis:
  enabled: false
config: |
  ...
  cache:
    redis:
      enabled: true
      host: your-external-redis-host.somewhere
      port: 6379
      db: 0
      password: ${REDIS_PASSWORD}

secretEnv:
  REDIS_PASSWORD: yourRedisSecret
```
