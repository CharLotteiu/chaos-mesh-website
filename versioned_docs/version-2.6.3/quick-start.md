---
title: Quick Start
---

import PickVersion from '@site/src/components/PickVersion'

import VerifyInstallation from './common/verify-installation.md'

import QuickRun from './common/quick-run.md'

This document describes how to start Chaos Mesh quickly in a test or local environment.

:::caution

**In this document, Chaos Mesh is installed via a script for quick trial only.**

If you need to install Chaos Mesh in the production environment or other strict non-test scenarios, it is recommended to use [Helm](https://helm.sh/). For more details, refer to [Installation using Helm](production-installation-using-helm.md).

:::

## Environment preparation

Please ensure that the Kubernetes cluster is deployed in the environment before the trial. If the Kubernetes cluster has not been deployed, you can refer to the links below to complete the deployment:

- [Kubernetes](https://kubernetes.io/docs/setup/)
- [minikube](https://minikube.sigs.k8s.io/docs/start/)
- [kind](https://kind.sigs.k8s.io/docs/user/quick-start/)
- [K3s](https://rancher.com/docs/k3s/latest/en/quick-start/)
- [Microk8s](https://microk8s.io/)

## Quick installation

To install Chaos Mesh in a test environment, run the following script:

<PickVersion>
{`curl -sSL https://mirrors.chaos-mesh.org/latest/install.sh | bash`}
</PickVersion>

:::note

- If the current environment is [kind](https://kind.sigs.k8s.io/), add the `--local kind` parameter at the end of the script.

  <PickVersion>
  {`curl -sSL https://mirrors.chaos-mesh.org/latest/install.sh | bash -s -- --local kind`}
  </PickVersion>

  If you want to specify a `kind` version, add the `--kind-version xx` parameter at the end of the script, for example:

  <PickVersion>
  {`curl -sSL https://mirrors.chaos-mesh.org/latest/install.sh | bash -s -- --local kind --kind-version v0.20.0`}
  </PickVersion>

- If the current environment is [K3s](https://k3s.io/), add the `--k3s` parameter at the end of the script.

  <PickVersion>
  {`curl -sSL https://mirrors.chaos-mesh.org/latest/install.sh | bash -s -- --k3s`}
  </PickVersion>

- If the current environment is [Microk8s](https://microk8s.io/), add the `--microk8s` parameter at the end of the script.

  <PickVersion>
  {`curl -sSL https://mirrors.chaos-mesh.org/latest/install.sh | bash -s -- --microk8s`}
  </PickVersion>

:::

After running this script, Chaos Mesh automatically installs the CustomResourceDefining (CRD) that matches the version, all required components, and related Service Account configurations.

For more installation details, refer to the source code of the [`install.sh`](https://github.com/chaos-mesh/chaos-mesh/blob/master/install.sh).

## Verify the installation

<VerifyInstallation />

## Run Chaos experiments

<QuickRun />

## Uninstall Chaos Mesh

To uninstall Chaos Mesh, execute the following command:

<PickVersion>
{`curl -sSL https://mirrors.chaos-mesh.org/latest/install.sh | bash -s -- --template | kubectl delete -f -`}
</PickVersion>

You can also delete the `chaos-mesh` namespace to directly uninstall Chaos Mesh:

```sh
kubectl delete ns chaos-mesh
```

## FAQ

### Why the `local` directory appears in the root directory after installation?

If you don't install `kind` in the existing environment, and you use the `--local kind` parameter when executing the installation command, the `install.sh` script will automatically install the `kind` in the `local` directory under the root directory.