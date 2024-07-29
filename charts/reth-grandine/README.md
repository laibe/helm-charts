# reth-grandine

![Version: 0.1.0](https://img.shields.io/badge/Version-0.1.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 1.0.3_0.4.1](https://img.shields.io/badge/AppVersion-1.0.3_0.4.1-informational?style=flat-square)

Helm chart for the reth execution client and grandine consensus client.

## Maintainers
| Name | Email | Url |
| ---- | ------ | --- |
| laibe |  | <https://github.com/laibe> |

## Source Code

* <https://github.com/paradigmxyz/reth>
* <https://github.com/status-im/grandine-eth2>

## Quick Start

```bash
# holesky testnet
helm install -n holesky reth-grandine-1 charts/reth-grandine --set global.network=holesky --set grandine.checkpointSync.enabled=true --set grandine.checkpointSync.url=https://holesky.beaconstate.info --set reth.ports.p2p=30002 --set grandine.ports.p2p=30003 --set global.persistence.size=200Gi
# mainnet
helm install -n mainnet reth-grandine-2 charts/reth-grandine --set global.network=mainnet --set grandine.checkpointSync.enabled=true --set grandine.checkpointSync.url=https://beaconstate.info --set reth.ports.p2p=30000 --set grandine.ports.p2p=30001 --set global.persistence.size=3500Gi
```

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| fullnameOverride | string | `""` | Overrides the chart's computed fullname |
| global.affinity | object | `{}` | Set affinity |
| global.engineRpcPort | int | `8551` | Engine API JSON-RPC Port |
| global.imagePullSecrets | object | `{}` | A list of pull secrets is used when credentials are needed to access a container registry with username and password. |
| global.network | string | `"holesky"` | Network name: mainnet, holesky, sepolia |
| global.nodeSelector | object | `{}` | Use nodeSelector in case you want to sync via rsync (init-rsync.enabled: true). E.g. kubernetes.io/hostname: <node-name> |
| global.persistence.accessModes | list | `["ReadWriteOnce"]` | Access mode for pvc |
| global.persistence.size | string | `"10Gi"` | Requested size the pvc (adjust for mainnet usage) |
| global.persistence.storageClassName | string | `nil` | Use a specific storage class. |
| global.podAnnotations | object | `{}` | Pod annotation to be added |
| global.podLabels | object | `{}` | Pod labels to be added |
| global.podMonitor.create | bool | `false` | Create a [PodMonitor](https://github.com/prometheus-operator/prometheus-operator/blob/main/Documentation/user-guides/getting-started.md) |
| global.securityContext | object | `{"fsGroup":1000,"runAsGroup":1000,"runAsNonRoot":true,"runAsUser":1000}` | Pod security context |
| global.service.annotations | object | `{}` | Service annotations |
| global.service.clusterIP | string | `"None"` | ClusterIP is set to None by default (headless service) |
| global.service.enabled | bool | `true` | Enable Service |
| global.service.type | string | `"ClusterIP"` | Service type, ClusterIP, LoadBalancer or ClusterIP. |
| global.serviceAccount.annotations | object | `{}` | Annotations to add to the service account |
| global.serviceAccount.create | bool | `true` | Enable service account (Note: Service Account will only be automatically created if `global.serviceAccount.name` is not set) |
| global.serviceAccount.name | string | `""` | Name of an already existing service account. Setting this value disables the automatic service account creation |
| global.terminationGracePeriodSeconds | int | `120` | Time for clean-shutdown, mainnet: 300 |
| global.tolerations | list | `[]` |  |
| global.updateStrategy.type | string | `"RollingUpdate"` | Update stategy type |
| grandine.checkpointSync.enabled | bool | `true` | Enable checkpoint sync |
| grandine.checkpointSync.url | string | `"https://beaconstate.info"` | Url of the trusted node |
| grandine.containerSecurityContext | object | `{}` |  |
| grandine.extBuilder.enabled | bool | `true` | enable external builder (mev-boost) |
| grandine.extBuilder.url | string | `"http://mev-boost:18500"` | url of external builder |
| grandine.image.pullPolicy | string | `"IfNotPresent"` |  |
| grandine.image.repository | string | `"sifrai/grandine"` | Container image repository |
| grandine.image.tag | string | `"unstable-amd64-0.4.0.rc0"` | Image tag |
| grandine.livenessProbe.initialDelaySeconds | int | `60` |  |
| grandine.livenessProbe.periodSeconds | int | `120` |  |
| grandine.livenessProbe.tcpSocket.port | int | `5052` | Liveness probe tcpSocket port, default is the grandine httpRest port. |
| grandine.name | string | `"grandine"` | Name of the container |
| grandine.podMonitor.interval | string | `"30s"` |  |
| grandine.podMonitor.path | string | `"/metrics"` |  |
| grandine.podMonitor.scrapeTimeout | string | `"10s"` |  |
| grandine.ports.metrics | int | `6061` |  |
| grandine.ports.p2p | int | `30002` | TCP and UDP P2P port: place in range 30000-32767 and verify that no existing nodes use these ports |
| grandine.ports.rest | int | `5052` | Beacon API port |
| grandine.readinessProbe.initialDelaySeconds | int | `60` |  |
| grandine.readinessProbe.periodSeconds | int | `10` |  |
| grandine.readinessProbe.tcpSocket.port | int | `5052` | Readiness probe tcpSocket port, default is the grandine httpRest port. |
| grandine.resources | object | `{"limits":{"cpu":"1000m","memory":"6Gi"},"requests":{"cpu":"1000m","memory":"6Gi"}}` | Resource requests and limits |
| initCommon.containerSecurityContext.runAsNonRoot | bool | `false` |  |
| initCommon.containerSecurityContext.runAsUser | int | `0` |  |
| initCommon.image.pullPolicy | string | `"IfNotPresent"` | Container pull policy |
| initCommon.image.repository | string | `"archlinux"` | Container image repository. Archlinux contains curl and openssl. |
| initCommon.image.tag | string | `"latest"` | Image tag |
| initCommon.name | string | `"init-common"` | Init container to set the correct permissions to access data directories and create the jwt file. |
| nameOverride | string | `""` | Overrides the chart's name |
| reth.containerSecurityContext.runAsGroup | int | `1000` |  |
| reth.containerSecurityContext.runAsNonRoot | bool | `true` |  |
| reth.containerSecurityContext.runAsUser | int | `1000` |  |
| reth.fullNode | object | `{"enabled":false}` | Run as full node (default is archive) |
| reth.image.pullPolicy | string | `"IfNotPresent"` | Container pull policy |
| reth.image.repository | string | `"ghcr.io/paradigmxyz/reth"` | Container image repository |
| reth.image.tag | string | `"v1.0.3"` | Image tag |
| reth.livenessProbe.initialDelaySeconds | int | `60` |  |
| reth.livenessProbe.periodSeconds | int | `120` |  |
| reth.livenessProbe.tcpSocket.port | int | `8545` | Liveness probe tcpSocket port |
| reth.logLevel | string | `"info"` | Rust log level: error, warn, info, debug, trace |
| reth.name | string | `"reth"` | Name of the container |
| reth.podMonitor.interval | string | `"30s"` |  |
| reth.podMonitor.path | string | `"/debug/metrics/prometheus"` |  |
| reth.podMonitor.scrapeTimeout | string | `"10s"` |  |
| reth.ports.metrics | int | `6060` | Metrics port |
| reth.ports.p2p | int | `30001` | TCP and UDP P2P port: place in range 30000-32767 and verify that no existing nodes use these ports |
| reth.ports.rpc | int | `8545` | Execution API port HTTP |
| reth.ports.ws | int | `8546` | Execution API port WebSockets |
| reth.readinessProbe.initialDelaySeconds | int | `60` |  |
| reth.readinessProbe.periodSeconds | int | `10` |  |
| reth.readinessProbe.tcpSocket.port | int | `8545` | Readiness probe tcpSocket port |
| reth.resources | object | `{"limits":{"cpu":"4000m","memory":"32Gi"},"requests":{"cpu":"4000m","memory":"32Gi"}}` | Resource requests and limits |
| reth.resources.limits.cpu | string | `"4000m"` | mainnet: 4000m |
| reth.resources.limits.memory | string | `"32Gi"` | mainnet: 32Gi |
| reth.resources.requests.cpu | string | `"4000m"` | mainnet: 4000m |
| reth.resources.requests.memory | string | `"32Gi"` | mainnet: 28Gi |
| reth.rpc.httpApi | list | `["debug","eth","net","trace","txpool","web3","rpc"]` | Api namespaces to enable: admin, debug, eth, net, trace, txpool, web3, rpc |
| reth.rpc.maxConnections | int | `100000` | Maximum number of RPC server connections |
| reth.rpc.maxRequestSize | int | `15` | Set the maximum RPC request payload size for both HTTP and WS in megabytes |
| reth.rpc.maxResponseSize | int | `500` | Set the maximum RPC response payload size for both HTTP and WS in megabytes |
| reth.rpc.maxSubscriptionsPerConnection | int | `1024` | Set the the maximum concurrent subscriptions per connection |
| reth.rpc.maxTracingRequests | int | `100` | Maximum number of concurrent tracing requests |
| reth.staticPeers | object | `{"enabled":false,"peers":[]}` | Static peers settings |
| reth.staticPeers.enabled | bool | `false` | Enable static peers. Switch added since reth does not accept empty string as argument for trusted-peers |
| reth.staticPeers.peers | list | `[]` | List of static peers (optional) |
