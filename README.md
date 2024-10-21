#### Create daemonset collector secret
```console
kubectl create secret generic elastic-secret-ds \                                    
     --from-literal=elastic_endpoint='https://blabla.es.us-central1.gcp.cloud.es.io' \
     --from-literal=elastic_api_key='lalallalala=='
```

#### Create deployment collector secret

```console
kubectl create secret generic elastic-secret \                                   
  --from-literal=elastic_apm_endpoint='blalkjsdflkxncv.apm.us-central1.gcp.cloud.es.io:443' \
  --from-literal=elastic_apm_secret_token='Bearer lsjdlkfjlksjdf93u9df'
```

#### Deploy the Opentelemetry Demo

```yaml
helm install -f deployment.yaml my-otel-demo open-telemetry/opentelemetry-demo
```

#### Deploy the daemonset Collector

```yaml
helm install daemonset open-telemetry/opentelemetry-collector --values daemonset.yaml
```

#### Deploy the sample logs application

```yaml
k apply -f ds-logs.yaml
```

#### Forward demo traffic

```yaml
kubectl --namespace default port-forward svc/my-otel-demo-frontendproxy 8080:8080
```