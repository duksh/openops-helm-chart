# OpenOps Helm Chart

A Helm chart for deploying OpenOps agent to Kubernetes

## Prerequisites

- Kubernetes 1.19+
- Helm 3.2.0+
- PV provisioner support in the underlying infrastructure (if persistence is enabled)

## Installing the Chart

```bash
helm install my-openops openops/openops
```

## Parameters

### Global parameters

| Name               | Description                                     | Value  |
|--------------------|------------------------------------------------|--------|
| `replicaCount`     | Number of OpenOps replicas to deploy           | `1`    |
| `image.repository` | OpenOps image repository                       | `public.ecr.aws/openops/agent` |
| `image.tag`        | OpenOps image tag                              | `latest` |
| `image.pullPolicy` | OpenOps image pull policy                      | `IfNotPresent` |

### Service parameters

| Name               | Description                                     | Value  |
|--------------------|------------------------------------------------|--------|
| `service.type`     | OpenOps service type                           | `ClusterIP` |
| `service.port`     | OpenOps service port                           | `80`   |

### Persistence parameters

| Name                       | Description                              | Value  |
|----------------------------|------------------------------------------|--------|
| `persistence.enabled`      | Enable persistence                       | `true` |
| `persistence.size`         | Storage size                             | `50Gi` |
| `persistence.storageClass` | Storage class (leave empty for default)  | `""`   |

### Credentials and Environment Variables

| Name                       | Description                               | Value  |
|----------------------------|-------------------------------------------|--------|
| `env.OPS_OPENOPS_ADMIN_EMAIL` | Admin email                           | `admin@example.com` |
| `secrets.enabled`           | Enable secret creation                  | `true` |
| `secrets.adminPassword`     | Admin password                          | `changeMe` |
