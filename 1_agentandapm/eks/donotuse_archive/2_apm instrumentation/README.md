# Pre-req for APM
- Make sure tracer related to Apache Skywalking is removed on the services for APM testing. 2 APM Tracers cannot coexist together.
- Please ensure this port 8000 is also allowed according to the document here (no action needed if there is no rules)
    - https://docs.datadoghq.com/containers/troubleshooting/admission-controller/?tab=helm#amazon-elastic-kubernetes-service-eks 

## Identify APM services to instrument
- Configure your Service Deployment.yaml for APM Instrumentation + DD Config
  - This has to be done for each deployment that you want to instrument APM for.
- Add following lines - line 4-7, line 29-31 
    - This is done for Datadog to Automatically Correlate in the platform - read here if needed - https://docs.datadoghq.com/getting_started/tagging/unified_service_tagging/?tab=kubernetes#full-configuration

- Add following lines line 24-27, line 35-38 for APM Installation

## Restart your service after changing yaml file
- This is required in order for APM to be installed
```
kubectl apply -f xxx.yaml 
```