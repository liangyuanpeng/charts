# Xline helm chart

Xline is a distributed KV storage for metadata management. Xline makes it possible to manage metadata, such as indexes, permissions, and configurations across multiple clusters.

[Overview of Xline](https://xline.cloud/)


## TL;DR

```shell
helm install my-release oci://ghcr.io/liangyuanpeng/charts/xline
```

## Introduction

This chart bootstraps a xline deployment on a Kubernetes cluster using the Helm package manager.

## Prerequisites

- Kubernetes 1.19+
- Helm 3.2.0+
- PV provisioner support in the underlying infrastructure


## Installing the Chart

To install the chart with the release name my-release:
```shell
helm install my-release oci://ghcr.io/liangyuanpeng/charts/xline
```

These commands deploy xline on the Kubernetes cluster in the default configuration. The Parameters section lists the parameters that can be configured during installation.
> Tip: List all releases using helm list

## Uninstalling the Chart

To uninstall/delete the my-release deployment:

```shell
helm delete my-release
```
The command removes all the Kubernetes components associated with the chart and deletes the release.


## Parameters

### Global parameters

| Name                      | Description                 | Value |
|---------------------------|-----------------------------| --- |
| `image.repository`                  | Container image registry    | `""` |
| `image.pullPolicy` | Container image pull policy | `""`  |
| `image.tag`     | Container image tag         | `""` |
