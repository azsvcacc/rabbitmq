<!--- app-name: RabbitMQ -->

# RabbitMQ packaged 

RabbitMQ is an open source general-purpose message broker that is designed for consistent, highly-available messaging scenarios (both synchronous and asynchronous).

[Overview of RabbitMQ](https://www.rabbitmq.com)

Trademarks: This software listing is packaged by Bitnami. The respective trademarks mentioned in the offering are owned by the respective companies, and use of them does not imply any affiliation or endorsement.

## TL;DR

```console
helm install rabbitmq oci://registry-1.docker.io/bitnamicharts/rabbitmq
```

## Introduction

This chart bootstraps a [RabbitMQ](https://github.com/bitnami/containers/tree/main/bitnami/rabbitmq) deployment on a [Kubernetes](https://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.

Bitnami charts can be used with [Kubeapps](https://kubeapps.dev/) for deployment and management of Helm Charts in clusters.

## Prerequisites

- Kubernetes 1.19+
- Helm 3.2.0+
- PV provisioner support in the underlying infrastructure

## Installing the Chart

To install the chart with the release name `rabbitmq`:

```console
helm install rabbitmq Rabbitmq_v1/
```

The command deploys RabbitMQ on the Kubernetes cluster in the default configuration. The [Parameters](#parameters) section lists the parameters that can be configured during installation.

> **Tip**: List all releases using `helm list`

## Uninstalling the Chart

To uninstall/delete the `rabbitmq` deployment:

```console
helm delete rabbitmq
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Parameters

### Global parameters

| Name                      | Description                                     | Value |
| ------------------------- | ----------------------------------------------- | ----- |
| `global.imageRegistry`    | Global Docker image registry                    | `""`  |
| `global.imagePullSecrets` | Global Docker registry secret names as an array | `[]`  |
| `global.storageClass`     | Global StorageClass for Persistent Volume(s)    | `""`  |

### RabbitMQ Image parameters

| Name                | Description                                                                                              | Value                  |
| ------------------- | -------------------------------------------------------------------------------------------------------- | ---------------------- |
| `image.registry`    | RabbitMQ image registry                                                                                  | `docker.io`            |
| `image.repository`  | RabbitMQ image repository                                                                                | `bitnami/rabbitmq`     |
| `image.tag`         | RabbitMQ image tag (immutable tags are recommended)                                                      | `3.11.13-debian-11-r0` |
| `image.digest`      | RabbitMQ image digest in the way sha256:aa.... Please note this parameter, if set, will override the tag | `""`                   |
| `image.pullPolicy`  | RabbitMQ image pull policy                                                                               | `IfNotPresent`         |
| `image.pullSecrets` | Specify docker-registry secret names as an array                                                         | `[]`                   |
| `image.debug`       | Set to true if you would like to see extra information on logs                                           | `false`                |

### Common parameters

| Name                                         | Description                                                                                                                                                             | Value                                             |
| -------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------- |
| `nameOverride`                               | String to partially override rabbitmq.fullname template (will maintain the release name)                                                                                | `""`                                              |
| `fullnameOverride`                           | String to fully override rabbitmq.fullname template                                                                                                                     | `""`                                              |
| `namespaceOverride`                          | String to fully override common.names.namespace                                                                                                                         | `""`                                              |
| `kubeVersion`                                | Force target Kubernetes version (using Helm capabilities if not set)                                                                                                    | `""`                                              |
| `clusterDomain`                              | Kubernetes Cluster Domain                                                                                                                                               | `cluster.local`                                   |
| `extraDeploy`                                | Array of extra objects to deploy with the release                                                                                                                       | `[]`                                              |
| `commonAnnotations`                          | Annotations to add to all deployed objects                                                                                                                              | `{}`                                              |
| `servicenameOverride`                        | String to partially override headless service name                                                                                                                      | `""`                                              |
| `commonLabels`                               | Labels to add to all deployed objects                                                                                                                                   | `{}`                                              |
| `serviceBindings.enabled`                    | Create secret for service binding (Experimental)                                                                                                                        | `false`                                           |
| `diagnosticMode.enabled`                     | Enable diagnostic mode (all probes will be disabled and the command will be overridden)                                                                                 | `false`                                           |
| `diagnosticMode.command`                     | Command to override all containers in the deployment                                                                                                                    | `["sleep"]`                                       |
| `diagnosticMode.args`                        | Args to override all containers in the deployment                                                                                                                       | `["infinity"]`                                    |
| `hostAliases`                                | Deployment pod host aliases                                                                                                                                             | `[]`                                              |
| `dnsPolicy`                                  | DNS Policy for pod                                                                                                                                                      | `""`                                              |
| `dnsConfig`                                  | DNS Configuration pod                                                                                                                                                   | `{}`                                              |
| `auth.username`                              | RabbitMQ application username                                                                                                                                           | `user`                                            |
| `auth.password`                              | RabbitMQ application password                                                                                                                                           | `""`                                              |
| `auth.securePassword`                        | Whether to set the RabbitMQ password securely. This is incompatible with loading external RabbitMQ definitions and 'true' when not setting the auth.password parameter. | `true`                                            |
| `auth.existingPasswordSecret`                | Existing secret with RabbitMQ credentials (must contain a value for `rabbitmq-password` key)                                                                            | `""`                                              |
| `auth.enableLoopbackUser`                    | Enable Loopback user access? Be advised, that enabling the loopback user is a possible security risk!                                                                   | `false`                                           |
| `auth.erlangCookie`                          | Erlang cookie to determine whether different nodes are allowed to communicate with each other                                                                           | `""`                                              |
| `auth.existingErlangSecret`                  | Existing secret with RabbitMQ Erlang cookie (must contain a value for `rabbitmq-erlang-cookie` key)                                                                     | `""`                                              |
| `auth.tls.enabled`                           | Enable TLS support on RabbitMQ                                                                                                                                          | `false`                                           |
| `auth.tls.autoGenerated`                     | Generate automatically self-signed TLS certificates                                                                                                                     | `false`                                           |
| `auth.tls.failIfNoPeerCert`                  | When set to true, TLS connection will be rejected if client fails to provide a certificate                                                                              | `true`                                            |
| `auth.tls.sslOptionsVerify`                  | Should [peer verification](https://www.rabbitmq.com/ssl.html#peer-verification) be enabled?                                                                             | `verify_peer`                                     |
| `auth.tls.sslOptionsPassword.enabled`        | Enable usage of password for private Key                                                                                                                                | `false`                                           |
| `auth.tls.sslOptionsPassword.existingSecret` | Name of existing Secret containing the sslOptionsPassword                                                                                                               | `""`                                              |
| `auth.tls.sslOptionsPassword.key`            | Enable Key referring to sslOptionsPassword in Secret specified in auth.tls.sslOptionsPassword.existingSecret                                                            | `""`                                              |
| `auth.tls.sslOptionsPassword.password`       | Use this string as Password. If set, auth.tls.sslOptionsPassword.existingSecret and auth.tls.sslOptionsPassword.key are ignored                                         | `""`                                              |
| `auth.tls.caCertificate`                     | Certificate Authority (CA) bundle content                                                                                                                               | `""`                                              |
| `auth.tls.serverCertificate`                 | Server certificate content                                                                                                                                              | `""`                                              |
| `auth.tls.serverKey`                         | Server private key content                                                                                                                                              | `""`                                              |
| `auth.tls.existingSecret`                    | Existing secret with certificate content to RabbitMQ credentials                                                                                                        | `""`                                              |
| `auth.tls.existingSecretFullChain`           | Whether or not the existing secret contains the full chain in the certificate (`tls.crt`). Will be used in place of `ca.cert` if `true`.                                | `false`                                           |
| `auth.tls.overrideCaCertificate`             | Existing secret with certificate content be mounted instead of the `ca.crt` coming from caCertificate or existingSecret/existingSecretFullChain.                        | `""`                                              |
| `logs`                                       | Path of the RabbitMQ server's Erlang log file. Value for the `RABBITMQ_LOGS` environment variable                                                                       | `-`                                               |
| `ulimitNofiles`                              | RabbitMQ Max File Descriptors                                                                                                                                           | `65536`                                           |
| `maxAvailableSchedulers`                     | RabbitMQ maximum available scheduler threads                                                                                                                            | `""`                                              |
| `onlineSchedulers`                           | RabbitMQ online scheduler threads                                                                                                                                       | `""`                                              |
| `memoryHighWatermark.enabled`                | Enable configuring Memory high watermark on RabbitMQ                                                                                                                    | `false`                                           |
| `memoryHighWatermark.type`                   | Memory high watermark type. Either `absolute` or `relative`                                                                                                             | `relative`                                        |
| `memoryHighWatermark.value`                  | Memory high watermark value                                                                                                                                             | `0.4`                                             |
| `plugins`                                    | List of default plugins to enable (should only be altered to remove defaults; for additional plugins use `extraPlugins`)                                                | `rabbitmq_management rabbitmq_peer_discovery_k8s` |
| `communityPlugins`                           | List of Community plugins (URLs) to be downloaded during container initialization                                                                                       | `""`                                              |
| `extraPlugins`                               | Extra plugins to enable (single string containing a space-separated list)                                                                                               | `rabbitmq_auth_backend_ldap`                      |
| `clustering.enabled`                         | Enable RabbitMQ clustering                                                                                                                                              | `true`                                            |
| `clustering.addressType`                     | Switch clustering mode. Either `ip` or `hostname`                                                                                                                       | `hostname`                                        |
| `clustering.rebalance`                       | Rebalance master for queues in cluster when new replica is created                                                                                                      | `false`                                           |
| `clustering.forceBoot`                       | Force boot of an unexpectedly shut down cluster (in an unexpected order).                                                                                               | `false`                                           |
| `clustering.partitionHandling`               | Switch Partition Handling Strategy. Either `autoheal` or `pause-minority` or `pause-if-all-down` or `ignore`                                                            | `autoheal`                                        |
| `loadDefinition.enabled`                     | Enable loading a RabbitMQ definitions file to configure RabbitMQ                                                                                                        | `false`                                           |
| `loadDefinition.file`                        | Name of the definitions file                                                                                                                                            | `/app/load_definition.json`                       |
| `loadDefinition.existingSecret`              | Existing secret with the load definitions file                                                                                                                          | `""`                                              |
| `command`                                    | Override default container command (useful when using custom images)                                                                                                    | `[]`                                              |
| `args`                                       | Override default container args (useful when using custom images)                                                                                                       | `[]`                                              |
| `lifecycleHooks`                             | Overwrite livecycle for the RabbitMQ container(s) to automate configuration before or after startup                                                                     | `{}`                                              |
| `terminationGracePeriodSeconds`              | Default duration in seconds k8s waits for container to exit before sending kill signal.                                                                                 | `120`                                             |
| `extraEnvVars`                               | Extra environment variables to add to RabbitMQ pods                                                                                                                     | `[]`                                              |
| `extraEnvVarsCM`                             | Name of existing ConfigMap containing extra environment variables                                                                                                       | `""`                                              |
| `extraEnvVarsSecret`                         | Name of existing Secret containing extra environment variables (in case of sensitive data)                                                                              | `""`                                              |
| `containerPorts.amqp`                        |                                                                                                                                                                         | `5672`                                            |
| `containerPorts.amqpTls`                     |                                                                                                                                                                         | `5671`                                            |
| `containerPorts.dist`                        |                                                                                                                                                                         | `25672`                                           |
| `containerPorts.manager`                     |                                                                                                                                                                         | `15672`                                           |
| `containerPorts.epmd`                        |                                                                                                                                                                         | `4369`                                            |
| `containerPorts.metrics`                     |                                                                                                                                                                         | `9419`                                            |
| `initScripts`                                | Dictionary of init scripts. Evaluated as a template.                                                                                                                    | `{}`                                              |
| `initScriptsCM`                              | ConfigMap with the init scripts. Evaluated as a template.                                                                                                               | `""`                                              |
| `initScriptsSecret`                          | Secret containing `/docker-entrypoint-initdb.d` scripts to be executed at initialization time that contain sensitive data. Evaluated as a template.                     | `""`                                              |
| `extraContainerPorts`                        | Extra ports to be included in container spec, primarily informational                                                                                                   | `[]`                                              |
| `configuration`                              | RabbitMQ Configuration file content: required cluster configuration                                                                                                     | `""`                                              |
| `tcpListenOptions.backlog`                   | Maximum size of the unaccepted TCP connections queue                                                                                                                    | `128`                                             |
| `tcpListenOptions.nodelay`                   | When set to true, deactivates Nagle's algorithm. Default is true. Highly recommended for most users.                                                                    | `true`                                            |
| `tcpListenOptions.linger.lingerOn`           | Enable Server socket lingering                                                                                                                                          | `true`                                            |
| `tcpListenOptions.linger.timeout`            | Server Socket lingering timeout                                                                                                                                         | `0`                                               |
| `tcpListenOptions.keepalive`                 | When set to true, enables TCP keepalives                                                                                                                                | `false`                                           |
| `configurationExistingSecret`                | Existing secret with the configuration to use as rabbitmq.conf.                                                                                                         | `""`                                              |
| `extraConfiguration`                         | Configuration file content: extra configuration to be appended to RabbitMQ configuration                                                                                | `""`                                              |
| `extraConfigurationExistingSecret`           | Existing secret with the extra configuration to append to `configuration`.                                                                                              | `""`                                              |
| `advancedConfiguration`                      | Configuration file content: advanced configuration                                                                                                                      | `""`                                              |
| `advancedConfigurationExistingSecret`        | Existing secret with the advanced configuration file (must contain a key `advanced.config`).                                                                            | `""`                                              |
| `featureFlags`                               | that controls what features are considered to be enabled or available on all cluster nodes.                                                                             | `""`                                              |
| `ldap.enabled`                               | Enable LDAP support                                                                                                                                                     | `false`                                           |
| `ldap.uri`                                   | LDAP connection string.                                                                                                                                                 | `""`                                              |
| `ldap.servers`                               | List of LDAP servers hostnames. This is valid only if ldap.uri is not set                                                                                               | `[]`                                              |
| `ldap.port`                                  | LDAP servers port. This is valid only if ldap.uri is not set                                                                                                            | `""`                                              |
| `ldap.userDnPattern`                         | Pattern used to translate the provided username into a value to be used for the LDAP bind.                                                                              | `""`                                              |
| `ldap.binddn`                                | DN of the account used to search in the LDAP server.                                                                                                                    | `""`                                              |
| `ldap.bindpw`                                | Password for binddn account.                                                                                                                                            | `""`                                              |
| `ldap.basedn`                                | Base DN path where binddn account will search for the users.                                                                                                            | `""`                                              |
| `ldap.uidField`                              | Field used to match with the user name (uid, samAccountName, cn, etc). It matches with 'dn_lookup_attribute' in RabbitMQ configuration                                  | `""`                                              |
| `ldap.uidField`                              | Field used to match with the user name (uid, samAccountName, cn, etc). It matches with 'dn_lookup_attribute' in RabbitMQ configuration                                  | `""`                                              |
| `ldap.authorisationEnabled`                  | Enable LDAP authorisation. Please set 'advancedConfiguration' with tag, topic, resources and vhost mappings                                                             | `false`                                           |
| `ldap.tls.enabled`                           | Enabled TLS configuration.                                                                                                                                              | `false`                                           |
| `ldap.tls.startTls`                          | Use STARTTLS instead of LDAPS.                                                                                                                                          | `false`                                           |
| `ldap.tls.skipVerify`                        | Skip any SSL verification (hostanames or certificates)                                                                                                                  | `false`                                           |
| `ldap.tls.verify`                            | Verify connection. Valid values are 'verify_peer' or 'verify_none'                                                                                                      | `verify_peer`                                     |
| `ldap.tls.certificatesMountPath`             | Where LDAP certifcates are mounted.                                                                                                                                     | `/opt/bitnami/rabbitmq/ldap/certs`                |
| `ldap.tls.certificatesSecret`                | Secret with LDAP certificates.                                                                                                                                          | `""`                                              |
| `ldap.tls.CAFilename`                        | CA certificate filename. Should match with the CA entry key in the ldap.tls.certificatesSecret.                                                                         | `""`                                              |
| `ldap.tls.certFilename`                      | Client certificate filename to authenticate against the LDAP server. Should match with certificate the entry key in the ldap.tls.certificatesSecret.                    | `""`                                              |
| `ldap.tls.certKeyFilename`                   | Client Key filename to authenticate against the LDAP server. Should match with certificate the entry key in the ldap.tls.certificatesSecret.                            | `""`                                              |
| `extraVolumeMounts`                          | Optionally specify extra list of additional volumeMounts                                                                                                                | `[]`                                              |
| `extraVolumes`                               | Optionally specify extra list of additional volumes .                                                                                                                   | `[]`                                              |
| `extraSecrets`                               | Optionally specify extra secrets to be created by the chart.                                                                                                            | `{}`                                              |
| `extraSecretsPrependReleaseName`             | Set this flag to true if extraSecrets should be created with <release-name> prepended.                                                                                  | `false`                                           |

### Statefulset parameters

| Name                                    | Description                                                                                                              | Value           |
| --------------------------------------- | ------------------------------------------------------------------------------------------------------------------------ | --------------- |
| `replicaCount`                          | Number of RabbitMQ replicas to deploy                                                                                    | `1`             |
| `schedulerName`                         | Use an alternate scheduler, e.g. "stork".                                                                                | `""`            |
| `podManagementPolicy`                   | Pod management policy                                                                                                    | `OrderedReady`  |
| `podLabels`                             | RabbitMQ Pod labels. Evaluated as a template                                                                             | `{}`            |
| `podAnnotations`                        | RabbitMQ Pod annotations. Evaluated as a template                                                                        | `{}`            |
| `updateStrategy.type`                   | Update strategy type for RabbitMQ statefulset                                                                            | `RollingUpdate` |
| `statefulsetLabels`                     | RabbitMQ statefulset labels. Evaluated as a template                                                                     | `{}`            |
| `statefulsetAnnotations`                | RabbitMQ statefulset annotations. Evaluated as a template                                                                | `{}`            |
| `priorityClassName`                     | Name of the priority class to be used by RabbitMQ pods, priority class needs to be created beforehand                    | `""`            |
| `podAffinityPreset`                     | Pod affinity preset. Ignored if `affinity` is set. Allowed values: `soft` or `hard`                                      | `""`            |
| `podAntiAffinityPreset`                 | Pod anti-affinity preset. Ignored if `affinity` is set. Allowed values: `soft` or `hard`                                 | `soft`          |
| `nodeAffinityPreset.type`               | Node affinity preset type. Ignored if `affinity` is set. Allowed values: `soft` or `hard`                                | `""`            |
| `nodeAffinityPreset.key`                | Node label key to match Ignored if `affinity` is set.                                                                    | `""`            |
| `nodeAffinityPreset.values`             | Node label values to match. Ignored if `affinity` is set.                                                                | `[]`            |
| `affinity`                              | Affinity for pod assignment. Evaluated as a template                                                                     | `{}`            |
| `nodeSelector`                          | Node labels for pod assignment. Evaluated as a template                                                                  | `{}`            |
| `tolerations`                           | Tolerations for pod assignment. Evaluated as a template                                                                  | `[]`            |
| `topologySpreadConstraints`             | Topology Spread Constraints for pod assignment spread across your cluster among failure-domains. Evaluated as a template | `[]`            |
| `podSecurityContext.enabled`            | Enable RabbitMQ pods' Security Context                                                                                   | `true`          |
| `podSecurityContext.fsGroup`            | Set RabbitMQ pod's Security Context fsGroup                                                                              | `1001`          |
| `containerSecurityContext.enabled`      | Enabled RabbitMQ containers' Security Context                                                                            | `true`          |
| `containerSecurityContext.runAsUser`    | Set RabbitMQ containers' Security Context runAsUser                                                                      | `1001`          |
| `containerSecurityContext.runAsNonRoot` | Set RabbitMQ container's Security Context runAsNonRoot                                                                   | `true`          |
| `resources.limits`                      | The resources limits for RabbitMQ containers                                                                             | `{}`            |
| `resources.requests`                    | The requested resources for RabbitMQ containers                                                                          | `{}`            |
| `livenessProbe.enabled`                 | Enable livenessProbe                                                                                                     | `true`          |
| `livenessProbe.initialDelaySeconds`     | Initial delay seconds for livenessProbe                                                                                  | `120`           |
| `livenessProbe.periodSeconds`           | Period seconds for livenessProbe                                                                                         | `30`            |
| `livenessProbe.timeoutSeconds`          | Timeout seconds for livenessProbe                                                                                        | `20`            |
| `livenessProbe.failureThreshold`        | Failure threshold for livenessProbe                                                                                      | `6`             |
| `livenessProbe.successThreshold`        | Success threshold for livenessProbe                                                                                      | `1`             |
| `readinessProbe.enabled`                | Enable readinessProbe                                                                                                    | `true`          |
| `readinessProbe.initialDelaySeconds`    | Initial delay seconds for readinessProbe                                                                                 | `10`            |
| `readinessProbe.periodSeconds`          | Period seconds for readinessProbe                                                                                        | `30`            |
| `readinessProbe.timeoutSeconds`         | Timeout seconds for readinessProbe                                                                                       | `20`            |
| `readinessProbe.failureThreshold`       | Failure threshold for readinessProbe                                                                                     | `3`             |
| `readinessProbe.successThreshold`       | Success threshold for readinessProbe                                                                                     | `1`             |
| `startupProbe.enabled`                  | Enable startupProbe                                                                                                      | `false`         |
| `startupProbe.initialDelaySeconds`      | Initial delay seconds for startupProbe                                                                                   | `10`            |
| `startupProbe.periodSeconds`            | Period seconds for startupProbe                                                                                          | `30`            |
| `startupProbe.timeoutSeconds`           | Timeout seconds for startupProbe                                                                                         | `20`            |
| `startupProbe.failureThreshold`         | Failure threshold for startupProbe                                                                                       | `3`             |
| `startupProbe.successThreshold`         | Success threshold for startupProbe                                                                                       | `1`             |
| `customLivenessProbe`                   | Override default liveness probe                                                                                          | `{}`            |
| `customReadinessProbe`                  | Override default readiness probe                                                                                         | `{}`            |
| `customStartupProbe`                    | Define a custom startup probe                                                                                            | `{}`            |
| `initContainers`                        | Add init containers to the RabbitMQ pod                                                                                  | `[]`            |
| `sidecars`                              | Add sidecar containers to the RabbitMQ pod                                                                               | `[]`            |
| `pdb.create`                            | Enable/disable a Pod Disruption Budget creation                                                                          | `false`         |
| `pdb.minAvailable`                      | Minimum number/percentage of pods that should remain scheduled                                                           | `1`             |
| `pdb.maxUnavailable`                    | Maximum number/percentage of pods that may be made unavailable                                                           | `""`            |

### RBAC parameters

| Name                                          | Description                                                                                | Value  |
| --------------------------------------------- | ------------------------------------------------------------------------------------------ | ------ |
| `serviceAccount.create`                       | Enable creation of ServiceAccount for RabbitMQ pods                                        | `true` |
| `serviceAccount.name`                         | Name of the created serviceAccount                                                         | `""`   |
| `serviceAccount.automountServiceAccountToken` | Auto-mount the service account token in the pod                                            | `true` |
| `serviceAccount.annotations`                  | Annotations for service account. Evaluated as a template. Only used if `create` is `true`. | `{}`   |
| `rbac.create`                                 | Whether RBAC rules should be created                                                       | `true` |

### Persistence parameters

| Name                        | Description                                      | Value                      |
| --------------------------- | ------------------------------------------------ | -------------------------- |
| `persistence.enabled`       | Enable RabbitMQ data persistence using PVC       | `true`                     |
| `persistence.storageClass`  | PVC Storage Class for RabbitMQ data volume       | `""`                       |
| `persistence.selector`      | Selector to match an existing Persistent Volume  | `{}`                       |
| `persistence.accessModes`   | PVC Access Modes for RabbitMQ data volume        | `["ReadWriteOnce"]`        |
| `persistence.existingClaim` | Provide an existing PersistentVolumeClaims       | `""`                       |
| `persistence.mountPath`     | The path the volume will be mounted at           | `/bitnami/rabbitmq/mnesia` |
| `persistence.subPath`       | The subdirectory of the volume to mount to       | `""`                       |
| `persistence.size`          | PVC Storage Request for RabbitMQ data volume     | `8Gi`                      |
| `persistence.annotations`   | Persistence annotations. Evaluated as a template | `{}`                       |
| `persistence.labels`        | Persistence labels. Evaluated as a template      | `{}`                       |

### Exposure parameters

| Name                               | Description                                                                                                                      | Value                    |
| ---------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- | ------------------------ |
| `service.type`                     | Kubernetes Service type                                                                                                          | `ClusterIP`              |
| `service.portEnabled`              | Amqp port. Cannot be disabled when `auth.tls.enabled` is `false`. Listener can be disabled with `listeners.tcp = none`.          | `true`                   |
| `service.distPortEnabled`          | Erlang distribution server port                                                                                                  | `true`                   |
| `service.managerPortEnabled`       | RabbitMQ Manager port                                                                                                            | `true`                   |
| `service.epmdPortEnabled`          | RabbitMQ EPMD Discovery service port                                                                                             | `true`                   |
| `service.ports.amqp`               | Amqp service port                                                                                                                | `5672`                   |
| `service.ports.amqpTls`            | Amqp TLS service port                                                                                                            | `5671`                   |
| `service.ports.dist`               | Erlang distribution service port                                                                                                 | `25672`                  |
| `service.ports.manager`            | RabbitMQ Manager service port                                                                                                    | `15672`                  |
| `service.ports.metrics`            | RabbitMQ Prometheues metrics service port                                                                                        | `9419`                   |
| `service.ports.epmd`               | EPMD Discovery service port                                                                                                      | `4369`                   |
| `service.portNames.amqp`           | Amqp service port name                                                                                                           | `amqp`                   |
| `service.portNames.amqpTls`        | Amqp TLS service port name                                                                                                       | `amqp-ssl`               |
| `service.portNames.dist`           | Erlang distribution service port name                                                                                            | `dist`                   |
| `service.portNames.manager`        | RabbitMQ Manager service port name                                                                                               | `http-stats`             |
| `service.portNames.metrics`        | RabbitMQ Prometheues metrics service port name                                                                                   | `metrics`                |
| `service.portNames.epmd`           | EPMD Discovery service port name                                                                                                 | `epmd`                   |
| `service.nodePorts.amqp`           | Node port for Ampq                                                                                                               | `""`                     |
| `service.nodePorts.amqpTls`        | Node port for Ampq TLS                                                                                                           | `""`                     |
| `service.nodePorts.dist`           | Node port for Erlang distribution                                                                                                | `""`                     |
| `service.nodePorts.manager`        | Node port for RabbitMQ Manager                                                                                                   | `""`                     |
| `service.nodePorts.epmd`           | Node port for EPMD Discovery                                                                                                     | `""`                     |
| `service.nodePorts.metrics`        | Node port for RabbitMQ Prometheues metrics                                                                                       | `""`                     |
| `service.extraPorts`               | Extra ports to expose in the service                                                                                             | `[]`                     |
| `service.loadBalancerSourceRanges` | Address(es) that are allowed when service is `LoadBalancer`                                                                      | `[]`                     |
| `service.externalIPs`              | Set the ExternalIPs                                                                                                              | `[]`                     |
| `service.externalTrafficPolicy`    | Enable client source IP preservation                                                                                             | `Cluster`                |
| `service.loadBalancerIP`           | Set the LoadBalancerIP                                                                                                           | `""`                     |
| `service.clusterIP`                | Kubernetes service Cluster IP                                                                                                    | `""`                     |
| `service.labels`                   | Service labels. Evaluated as a template                                                                                          | `{}`                     |
| `service.annotations`              | Service annotations. Evaluated as a template                                                                                     | `{}`                     |
| `service.annotationsHeadless`      | Headless Service annotations. Evaluated as a template                                                                            | `{}`                     |
| `service.headless.annotations`     | Annotations for the headless service.                                                                                            | `{}`                     |
| `service.sessionAffinity`          | Session Affinity for Kubernetes service, can be "None" or "ClientIP"                                                             | `None`                   |
| `service.sessionAffinityConfig`    | Additional settings for the sessionAffinity                                                                                      | `{}`                     |
| `ingress.enabled`                  | Enable ingress resource for Management console                                                                                   | `false`                  |
| `ingress.path`                     | Path for the default host. You may need to set this to '/*' in order to use this with ALB ingress controllers.                   | `/`                      |
| `ingress.pathType`                 | Ingress path type                                                                                                                | `ImplementationSpecific` |
| `ingress.hostname`                 | Default host for the ingress resource                                                                                            | `rabbitmq.local`         |
| `ingress.annotations`              | Additional annotations for the Ingress resource. To enable certificate autogeneration, place here your cert-manager annotations. | `{}`                     |
| `ingress.tls`                      | Enable TLS configuration for the hostname defined at `ingress.hostname` parameter                                                | `false`                  |
| `ingress.selfSigned`               | Set this to true in order to create a TLS secret for this ingress record                                                         | `false`                  |
| `ingress.extraHosts`               | The list of additional hostnames to be covered with this ingress record.                                                         | `[]`                     |
| `ingress.extraPaths`               | An array with additional arbitrary paths that may need to be added to the ingress under the main host                            | `[]`                     |
| `ingress.extraRules`               | The list of additional rules to be added to this ingress record. Evaluated as a template                                         | `[]`                     |
| `ingress.extraTls`                 | The tls configuration for additional hostnames to be covered with this ingress record.                                           | `[]`                     |
| `ingress.secrets`                  | Custom TLS certificates as secrets                                                                                               | `[]`                     |
| `ingress.ingressClassName`         | IngressClass that will be be used to implement the Ingress (Kubernetes 1.18+)                                                    | `""`                     |
| `ingress.existingSecret`           | It is you own the certificate as secret.                                                                                         | `""`                     |
| `networkPolicy.enabled`            | Enable creation of NetworkPolicy resources                                                                                       | `false`                  |
| `networkPolicy.allowExternal`      | Don't require client label for connections                                                                                       | `true`                   |
| `networkPolicy.additionalRules`    | Additional NetworkPolicy Ingress "from" rules to set. Note that all rules are OR-ed.                                             | `[]`                     |

### Metrics Parameters

| Name                                       | Description                                                                            | Value                 |
| ------------------------------------------ | -------------------------------------------------------------------------------------- | --------------------- |
| `metrics.enabled`                          | Enable exposing RabbitMQ metrics to be gathered by Prometheus                          | `false`               |
| `metrics.plugins`                          | Plugins to enable Prometheus metrics in RabbitMQ                                       | `rabbitmq_prometheus` |
| `metrics.podAnnotations`                   | Annotations for enabling prometheus to access the metrics endpoint                     | `{}`                  |
| `metrics.serviceMonitor.enabled`           | Create ServiceMonitor Resource for scraping metrics using PrometheusOperator           | `false`               |
| `metrics.serviceMonitor.namespace`         | Specify the namespace in which the serviceMonitor resource will be created             | `""`                  |
| `metrics.serviceMonitor.interval`          | Specify the interval at which metrics should be scraped                                | `30s`                 |
| `metrics.serviceMonitor.scrapeTimeout`     | Specify the timeout after which the scrape is ended                                    | `""`                  |
| `metrics.serviceMonitor.jobLabel`          | The name of the label on the target service to use as the job name in prometheus.      | `""`                  |
| `metrics.serviceMonitor.relabelings`       | RelabelConfigs to apply to samples before scraping.                                    | `[]`                  |
| `metrics.serviceMonitor.metricRelabelings` | MetricsRelabelConfigs to apply to samples before ingestion.                            | `[]`                  |
| `metrics.serviceMonitor.honorLabels`       | honorLabels chooses the metric's labels on collisions with target labels               | `false`               |
| `metrics.serviceMonitor.targetLabels`      | Used to keep given service's labels in target                                          | `{}`                  |
| `metrics.serviceMonitor.podTargetLabels`   | Used to keep given pod's labels in target                                              | `{}`                  |
| `metrics.serviceMonitor.path`              | Define the path used by ServiceMonitor to scrap metrics                                | `""`                  |
| `metrics.serviceMonitor.selector`          | ServiceMonitor selector labels                                                         | `{}`                  |
| `metrics.serviceMonitor.labels`            | Extra labels for the ServiceMonitor                                                    | `{}`                  |
| `metrics.serviceMonitor.annotations`       | Extra annotations for the ServiceMonitor                                               | `{}`                  |
| `metrics.prometheusRule.enabled`           | Set this to true to create prometheusRules for Prometheus operator                     | `false`               |
| `metrics.prometheusRule.additionalLabels`  | Additional labels that can be used so prometheusRules will be discovered by Prometheus | `{}`                  |
| `metrics.prometheusRule.namespace`         | namespace where prometheusRules resource should be created                             | `""`                  |
| `metrics.prometheusRule.rules`             | List of rules, used as template by Helm.                                               | `[]`                  |

### Init Container Parameters

| Name                                                   | Description                                                                                                                       | Value                   |
| ------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------- | ----------------------- |
| `volumePermissions.enabled`                            | Enable init container that changes the owner and group of the persistent volume(s) mountpoint to `runAsUser:fsGroup`              | `false`                 |
| `volumePermissions.image.registry`                     | Init container volume-permissions image registry                                                                                  | `docker.io`             |
| `volumePermissions.image.repository`                   | Init container volume-permissions image repository                                                                                | `bitnami/bitnami-shell` |
| `volumePermissions.image.tag`                          | Init container volume-permissions image tag                                                                                       | `11-debian-11-r102`     |
| `volumePermissions.image.digest`                       | Init container volume-permissions image digest in the way sha256:aa.... Please note this parameter, if set, will override the tag | `""`                    |
| `volumePermissions.image.pullPolicy`                   | Init container volume-permissions image pull policy                                                                               | `IfNotPresent`          |
| `volumePermissions.image.pullSecrets`                  | Specify docker-registry secret names as an array                                                                                  | `[]`                    |
| `volumePermissions.resources.limits`                   | Init container volume-permissions resource limits                                                                                 | `{}`                    |
| `volumePermissions.resources.requests`                 | Init container volume-permissions resource requests                                                                               | `{}`                    |
| `volumePermissions.containerSecurityContext.runAsUser` | User ID for the init container                                                                                                    | `0`                     |



```console
helm install rabbitmq \
  --set auth.username=admin,auth.password=secretpassword,auth.erlangCookie=secretcookie \
   helm_rabbitmq_v1

```console
helm install my-release -f values.yaml helm_rabbitmq_v1
