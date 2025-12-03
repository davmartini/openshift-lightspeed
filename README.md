## OpenShift LightSpeed Configuration

## With IBM Cloud
```
apiVersion: ols.openshift.io/v1alpha1
kind: OLSConfig
metadata:
  name: cluster
spec:
  llm:
    providers:
      - credentialsSecretRef:
          name: watsonx-api-keys                            ## kubernetes secret with IBM API KEY
        models:
          - name: ibm/granite-4-h-small                     ## model deployed on IBM Cloud and used by LightSpeed
        name: myWatsonX
        projectID: df7a53c5-4e20-4c0e-9c36-ff3b68c8d43b
        type: watsonx
        url: 'https://eu-de.ml.cloud.ibm.com'               ## IBM Cloud inference endpoint
  ols:
    defaultModel: ibm/granite-4-h-small                     ## model deployed on IBM Cloud and used by LightSpeed
    defaultProvider: myWatsonX                              ## Name of my provider
    introspectionEnabled: true                              ## Enable the possibility than OpenShift LightSpeed can interact directlly with the OpenShift cluster
    logLevel: INFO
```

## With RHOAI
```
apiVersion: ols.openshift.io/v1alpha1
kind: OLSConfig
metadata:
  name: cluster
spec:
  llm:
    providers:
    - credentialsSecretRef:
        name: rhoai-api-keys
      models:
      - name: granite-31-8b-lab-v1
      name: myRHOAI
      type: rhoai_vllm
      url: 'https://granite-31-8b-lab-v1-dmartini.apps.cluster-z4kvw.z4kvw.sandbox5419.opentlc.com:443/v1'
  ols:
    hideIcon: false
    introspectionEnabled: false                            
    logLevel: INFO 
    defaultProvider: myRHOAI
    defaultModel: granite-31-8b-lab-v1
```