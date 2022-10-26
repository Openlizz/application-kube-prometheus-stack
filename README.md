<h1 align="center">Lizz compatible Kube Prometheus Stack application</h1>

Lizz compatible application to add the [kube-prometheus stack](https://github.com/prometheus-community/helm-charts/tree/main/charts/kube-prometheus-stack) to a Lizz managed Kubernetes cluster.

To learn more about Lizz, see the [documentation](https://openlizz.com).

## Requirements

To add the application, you first need to have a [Kubernetes cluster initialized with Lizz](https://openlizz.com/docs/guides/init).
You also need to have the [Lizz CLI installed](https://openlizz.com/docs/installation).

## Add the application

To add the application to your cluster, run the following:

```bash
lizz add github \
    --owner=$GITHUB_USER  \
    --fleet=fleet \
    --origin-url=https://github.com/openlizz/application-kube-prometheus-stack \
    --path=./default \
    --destination=nextcloud \
    --cluster-role \
    --personal
```

Check the [guide](https://openlizz.com/docs/guides/add) to understand how works the lizz add command.

> **Note**
> You can adapt the command depending on your use case. See the [command API](https://openlizz.com/docs/cli/lizz_add_github) for more information.

> **Note**
> If you have a k3s cluster, use `--path=./k3s`. This requires to:
>
> - configure the master k3s node to expose metrics, refer to https://fabianlee.org/2022/07/02/prometheus-installing-kube-prometheus-stack-on-k3s-cluster/ and https://github.com/k3s-io/k3s/issues/3619#issuecomment-973188304,
> - set the `masterIp` value with the IP address of your k3s master node: `--set-value masterIp=<ip address of your k3s master node>`.

Reconcile the fleet repository to deploy the application using [Flux](https://fluxcd.io/):

```
flux reconcile source git flux-system
```

Check the pods with:

```
kubectl get pod -n monitoring
```

The output should be similar to:

```
NAMESPACE       NAME                                        READY   STATUS    RESTARTS      AGE
```

## Usage

Refer to the project documentation.

## Acknowledgements

This repository is only a wrapper to the [Helm chart](https://github.com/prometheus-community/helm-charts/tree/main/charts/kube-prometheus-stack) of the Kube Prometheus Stack to help its deployment in a Kubernetes cluster managed by Lizz.

Therefore, the credit goes to the developers and maintainers of the application and the chart.
