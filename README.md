# aks-aad-pod-identity-flux

Flux-managed repo to keep AKS AAD Pod Identity deployment configs

Assign Azure Active Directory Identities to kubernetes applications. This repository is a fork of https://github.com/Azure/aad-pod-identity and RBC added kustomizations & flux configurations

For more details about how aad-pod-identity works:
* https://github.com/Azure/aad-pod-identity
* https://github.com/Azure/aad-pod-identity/blob/master/docs/design/concept.png
* https://github.com/Azure/aad-pod-identity/blob/master/docs/design/concept.md

## Directory Structure

### Per-cluster configurations

The default template structure uses the following Kustomize overlays for applying per-cluster resources. This is used for configurations that are expected to be unique per cluster or namespace (such as RBAC, network policy, etc).

This structure assumes the default `FLUX_GIT_PATH` variable is used during installation of Flux:

```bash
FLUX_GIT_PATH="kustomize/${ENVIRONMENT}/${LOCATION}/${AKS_NAME}"
```

Per-cluster configurations are organized using the following structure:

```bash
$ tree kustomize/
kustomize/
└── global
    ├── kustomization.yaml
    └── <platform-global-resources...>.yaml
...
└── <service_tier>
    └── <region>
        └── <cluster_name>
            ├── namespaces
            │   └── <namespace_name>
            │       └── <namespace-specific-resources...>.yaml
            ├── kustomization.yaml
            └── <resource-manifests...>.yaml
```
