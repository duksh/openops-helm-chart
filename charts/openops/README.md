# OpenOps Helm Chart

A Helm chart for deploying the complete OpenOps platform to Kubernetes

## Version History

- 0.1.0: Initial release with core functionality
  - Deployment configuration for single OpenOps component
  - Service exposure
  - Secret management
  - Persistent volume integration
- 0.2.0: Enhanced multi-component architecture
  - Full deployment of all OpenOps components (app, engine, tables, analytics)
  - Integration with Postgres and Redis dependencies
  - NGINX gateway for unified access
  - Comprehensive configuration options for each component

## Prerequisites

- Kubernetes 1.19+
- Helm 3.2.0+
- PV provisioner support in the underlying infrastructure (for persistence)

## Installing the Chart

```bash
helm install my-openops openops/openops
```

## Architecture

This Helm chart deploys the complete OpenOps platform with the following components:

- **OpenOps App**: The main application component
- **OpenOps Engine**: The execution engine for automation workflows
- **OpenOps Tables**: Data storage and management component
- **OpenOps Analytics**: Analytics and reporting dashboard
- **Postgres**: Database for persistent storage
- **Redis**: In-memory cache and message broker
- **NGINX**: Gateway that routes traffic to the appropriate components

## Parameters

### Global parameters

| Name                  | Description                                        | Value  |
|-----------------------|----------------------------------------------------|--------|
| `nameOverride`        | Override the name of the chart                     | `""`   |
| `fullnameOverride`    | Override the full name of the chart                | `""`   |
| `global.storageClass` | Global storage class for persistent volumes        | `""`   |

### OpenOps App parameters

| Name                       | Description                                    | Value  |
|----------------------------|------------------------------------------------|--------|
| `app.enabled`              | Enable OpenOps App component                   | `true` |
| `app.replicaCount`         | Number of OpenOps App replicas                 | `1`    |
| `app.image.repository`     | OpenOps App image repository                   | `public.ecr.aws/openops/openops-app` |
| `app.image.tag`            | OpenOps App image tag                          | `0.2.7` |
| `app.image.pullPolicy`     | OpenOps App image pull policy                  | `IfNotPresent` |
| `app.service.type`         | OpenOps App service type                       | `ClusterIP` |
| `app.service.port`         | OpenOps App service port                       | `80`   |
| `app.resources.requests.cpu` | CPU request for OpenOps App                  | `1`    |
| `app.resources.requests.memory` | Memory request for OpenOps App            | `2Gi`  |
| `app.resources.limits.cpu` | CPU limit for OpenOps App                      | `2`    |
| `app.resources.limits.memory` | Memory limit for OpenOps App                | `4Gi`  |

### OpenOps Engine parameters

| Name                       | Description                                    | Value  |
|----------------------------|------------------------------------------------|--------|
| `engine.enabled`           | Enable OpenOps Engine component                | `true` |
| `engine.replicaCount`      | Number of OpenOps Engine replicas              | `1`    |
| `engine.image.repository`  | OpenOps Engine image repository                | `public.ecr.aws/openops/openops-engine` |
| `engine.image.tag`         | OpenOps Engine image tag                       | `0.2.7` |
| `engine.image.pullPolicy`  | OpenOps Engine image pull policy               | `IfNotPresent` |
| `engine.volumes.azure.enabled` | Enable Azure CLI volume                    | `true` |
| `engine.volumes.azure.size` | Azure CLI volume size                         | `1Gi`  |
| `engine.volumes.gcloud.enabled` | Enable Google Cloud SDK volume            | `true` |
| `engine.volumes.gcloud.size` | Google Cloud SDK volume size                 | `1Gi`  |

### OpenOps Tables parameters

| Name                       | Description                                    | Value  |
|----------------------------|------------------------------------------------|--------|
| `tables.enabled`           | Enable OpenOps Tables component                | `true` |
| `tables.replicaCount`      | Number of OpenOps Tables replicas              | `1`    |
| `tables.image.repository`  | OpenOps Tables image repository                | `public.ecr.aws/openops/openops-tables` |
| `tables.image.tag`         | OpenOps Tables image tag                       | `0.1.8` |
| `tables.image.pullPolicy`  | OpenOps Tables image pull policy               | `IfNotPresent` |
| `tables.service.type`      | OpenOps Tables service type                    | `ClusterIP` |
| `tables.service.port`      | OpenOps Tables service port                    | `80`   |
| `tables.persistence.enabled` | Enable persistence for Tables                | `true` |
| `tables.persistence.size`  | Storage size for Tables                        | `10Gi` |

### OpenOps Analytics parameters

| Name                       | Description                                    | Value  |
|----------------------------|------------------------------------------------|--------|
| `analytics.enabled`        | Enable OpenOps Analytics component             | `true` |
| `analytics.replicaCount`   | Number of OpenOps Analytics replicas           | `1`    |
| `analytics.image.repository` | OpenOps Analytics image repository           | `public.ecr.aws/openops/openops-analytics` |
| `analytics.image.tag`      | OpenOps Analytics image tag                    | `0.12.16` |
| `analytics.image.pullPolicy` | OpenOps Analytics image pull policy          | `IfNotPresent` |
| `analytics.service.type`   | OpenOps Analytics service type                 | `ClusterIP` |
| `analytics.service.port`   | OpenOps Analytics service port                 | `80`   |

### Postgres parameters

| Name                       | Description                                    | Value  |
|----------------------------|------------------------------------------------|--------|
| `postgres.enabled`         | Enable Postgres                                | `true` |
| `postgres.image.repository` | Postgres image repository                     | `postgres` |
| `postgres.image.tag`       | Postgres image tag                             | `14.4` |
| `postgres.service.port`    | Postgres service port                          | `5432` |
| `postgres.persistence.enabled` | Enable persistence for Postgres            | `true` |
| `postgres.persistence.size` | Storage size for Postgres                     | `20Gi` |
| `postgres.maxConnections`  | Maximum number of database connections         | `300`  |

### Redis parameters

| Name                       | Description                                    | Value  |
|----------------------------|------------------------------------------------|--------|
| `redis.enabled`            | Enable Redis                                   | `true` |
| `redis.image.repository`   | Redis image repository                         | `redis` |
| `redis.image.tag`          | Redis image tag                                | `7.4.0` |
| `redis.service.port`       | Redis service port                             | `6379` |
| `redis.persistence.enabled` | Enable persistence for Redis                  | `true` |
| `redis.persistence.size`   | Storage size for Redis                         | `5Gi`  |

### NGINX Gateway parameters

| Name                       | Description                                    | Value  |
|----------------------------|------------------------------------------------|--------|
| `nginx.enabled`            | Enable NGINX Gateway                           | `true` |
| `nginx.image.repository`   | NGINX image repository                         | `nginx` |
| `nginx.image.tag`          | NGINX image tag                                | `1.27.4` |
| `nginx.service.type`       | NGINX service type                             | `ClusterIP` |
| `nginx.service.port`       | NGINX service port                             | `80`   |
| `nginx.configMap.enabled`  | Enable NGINX configuration                     | `true` |

### Ingress parameters

| Name                      | Description                                     | Value  |
|---------------------------|-------------------------------------------------|--------|
| `ingress.enabled`         | Enable ingress for OpenOps                      | `false` |
| `ingress.className`       | Ingress class name                              | `""`   |
| `ingress.annotations`     | Ingress annotations                             | `{}`   |
| `ingress.hosts[0].host`   | Hostname for OpenOps                            | `openops.local` |
| `ingress.hosts[0].paths[0].path` | Path for the host                         | `/`     |
| `ingress.hosts[0].paths[0].pathType` | Path type                            | `ImplementationSpecific` |
| `ingress.tls`             | TLS configuration                               | `[]`   |

### Environment and Secret parameters

| Name                         | Description                                  | Value  |
|------------------------------|----------------------------------------------|--------|
| `env.OPS_OPENOPS_ADMIN_EMAIL` | Admin email address                         | `admin@example.com` |
| `secrets.enabled`            | Enable secret creation                       | `true` |
| `secrets.OPS_OPENOPS_ADMIN_PASSWORD` | Admin password                       | `changeMe` |
| `secrets.OPS_POSTGRES_USERNAME` | Postgres username                         | `postgres` |
| `secrets.OPS_POSTGRES_PASSWORD` | Postgres password                         | `postgres` |
| `secrets.OPS_ENCRYPTION_KEY` | Encryption key                               | `changeMe` |
| `secrets.OPS_JWT_SECRET` | JWT signing key                                 | `changeMe` |
