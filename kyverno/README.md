## Example cli output


```bash
kyverno apply policies/ --resource manifests/working.yaml

Applying 11 policy rules to 2 resources...

skipped mutate policy add-imagepullsecrets -> resource default/Deployment/nginx-deployment
pass: 5, fail: 0, warn: 0, error: 0, skip: 33 
```

***

```bash
kyverno apply policies/ --resource manifests/broken.yaml

Applying 11 policy rules to 2 resources...

skipped mutate policy add-imagepullsecrets -> resource default/Deployment/nginx-deployment
policy check-deprecated-apis -> resource default/StorageClass/standard failed: 
1. validate-v1-22-removals: storage.k8s.io/v1beta1/StorageClass is deprecated and will be removed in v1.22. See: https://kubernetes.io/docs/reference/using-api/deprecation-guide/ 

policy not-allow-latest -> resource default/Deployment/nginx-deployment failed: 
2. autogen-not-allow-latest: validation error: Using a mutable image tag e.g. 'latest' is not allowed. rule autogen-not-allow-latest failed at path /spec/template/spec/containers/0/image/ 

policy required-component-label -> resource default/Deployment/nginx-deployment failed: 
1. required-component-label: validation error: Required component label. rule required-component-label failed at path /metadata/labels/ 

policy require-requests-limits -> resource default/Deployment/nginx-deployment failed: 
1. required-resources-request-limit: validation error: CPU and memory resource requests and limits are required. rule required-resources-request-limit failed at path /spec/template/spec/containers/0/resources/ 

policy only-trustworthy-registries -> resource default/Deployment/nginx-deployment failed: 
1. autogen-validate-registries: validation error: Unknown image registry. rule autogen-validate-registries failed at path /spec/template/spec/containers/0/image/ 

pass: 1, fail: 5, warn: 0, error: 0, skip: 32 
```
