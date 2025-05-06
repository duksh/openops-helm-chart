# Changelog

## Version 0.2.0 (2025-05-06)

### Major Changes
- Completely redesigned the Helm chart to deploy the full OpenOps platform
- Added support for all OpenOps components: App, Engine, Tables, and Analytics
- Integrated with Postgres and Redis dependencies 
- Added NGINX gateway for unified access
- Updated image references to use official OpenOps images from ECR public registry

### Components
- OpenOps App: `public.ecr.aws/openops/openops-app:0.2.7`
- OpenOps Engine: `public.ecr.aws/openops/openops-engine:0.2.7`
- OpenOps Tables: `public.ecr.aws/openops/openops-tables:0.1.8`
- OpenOps Analytics: `public.ecr.aws/openops/openops-analytics:0.12.16`
- Postgres: `postgres:14.4`
- Redis: `redis:7.4.0`
- NGINX: `nginx:1.27.4`

### Configuration Changes
- Added component-specific configurations
- Global storage class settings
- Comprehensive environment variables for inter-component communication
- Centralized secret management

## Version 0.1.0 (2025-05-06)

### Initial Release
- Basic Helm chart for OpenOps agent deployment
- Single component architecture
- Basic service exposure
- Simple secret management
- PVC integration
