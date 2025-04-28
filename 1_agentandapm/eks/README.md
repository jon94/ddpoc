# EKS Agent Installation
- Official Datadog Document: https://docs.datadoghq.com/containers/kubernetes/installation/?tab=helm#installation

### values.yaml

- Feel free to use the values.yaml file that is provided in the repo.
- This configuration will turn on Infra, APM Collection, Log Collection, Network performance Monitoring, Universal Service Monitoring

# Pre-req for APM
- Make sure tracer related to Apache Skywalking is removed on the services for APM testing. 2 APM Tracers cannot coexist together.
- Please ensure this port 8000 is also allowed according to the document here (no action needed if there is no rules)
    - https://docs.datadoghq.com/containers/troubleshooting/admission-controller/?tab=helm#amazon-elastic-kubernetes-service-eks 

### Things take note for values.yaml
- Obtain API Key from https://app.datadoghq.com/organization-settings/api-keys
- Obtain APP Key from https://app.datadoghq.com/organization-settings/application-keys
- This will be used in the step below when creating datadog-secret
- replace clusterName (e.g. poccluster)
- replace `<NAMESPACE1>` and `<NAMESPACE2>` with the namespace that you want to instrument

### Creating Datadog API Key and APP Key as Kubernetes Secret
```
kubectl create namespace datadog
kubectl create secret generic datadog-secret -n datadog --from-literal api-key=<DATADOG_API_KEY> --from-literal app-key=<DATADOG_APP_KEY>
```

### Install via helm
```
helm repo add datadog https://helm.datadoghq.com
helm repo update
helm install datadog datadog/datadog -n datadog -f /dir/folder1/values.yaml
```

### If there are any changes to values.yaml
- Make changes to values.yaml
- Run the following after changes.
```
helm upgrade datadog datadog/datadog -n datadog -f /dir/folder1/values.yaml
```

### Validation
Once done, you should be able to view information on https://app.datadoghq.com/orchestration/explorer/pod?explorer-na-groups=false 