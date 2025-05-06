# OpenOps Helm Chart

This repository hosts the Helm chart for deploying OpenOps to Kubernetes clusters.

## What is OpenOps?

OpenOps is a No-Code FinOps automation platform that provides customizable workflows to automate various FinOps processes, such as cost optimization, budgeting, forecasting, allocation, and tagging. It enables collaboration between FinOps teams and stakeholders like engineers, DevOps, finance, and leadership.

## Usage

Add the Helm repository:

```bash
helm repo add openops https://duksh.github.io/openops-helm-chart
helm repo update
```

Install the OpenOps chart:

```bash
helm install my-openops openops/openops -f my-values.yaml
```

## Configuration

See the [values.yaml](./charts/openops/values.yaml) file for configurable parameters and the chart [README](./charts/openops/README.md) for detailed documentation.

## Requirements

- Kubernetes 1.19+
- Helm 3.2.0+
- PV provisioner support in the underlying infrastructure (if persistence is enabled)

## GitHub Pages and Chart Distribution

This repository uses the [Chart Releaser Action](https://github.com/helm/chart-releaser-action) to automatically package and release Helm charts on GitHub Pages when changes are pushed to the main branch.