# EKS Agent Installation

- Please go through this [guided tour](https://datadog.navattic.com/ui10b8i) to see how you can install and validate the agent on a kubernetes based set up, *I recommend using Helm instead of Operator*.
- Official Datadog Document: https://docs.datadoghq.com/containers/kubernetes/installation/?tab=helm#installation

## eks-values.yaml

- Feel free to use the eks-values.yaml file that is provided in the repo.
- This configuration will turn on Infra, APM Collection, Log Collection, Network performance Monitoring, Universal Service Monitoring

### Creating Datadog API Key and APP Key as Kubernetes Secret
```
kubectl create namespace datadog
kubectl create secret generic datadog-secret -n datadog --from-literal api-key=<DATADOG_API_KEY> --from-literal app-key=<DATADOG_APP_KEY>
```

### Install via helm
```
helm repo add datadog https://helm.datadoghq.com
helm repo update
helm install datadog datadog/datadog -n datadog -f /dir/toyour/values.yaml
```

### If there are any changes to values.yaml
- Make changes to values.yaml
- Run the following after changes.
```
helm upgrade datadog datadog/datadog -n datadog -f /dir/toyour/values.yaml
```

### Validation
Once done, you should be able to view information on https://app.datadoghq.com/orchestration/explorer/pod?explorer-na-groups=false 