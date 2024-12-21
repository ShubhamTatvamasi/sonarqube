# k8s

ID: admin \
Pass: admin

```bash
helm repo add sonarqube https://SonarSource.github.io/helm-chart-sonarqube
helm repo update
kubectl create namespace sonarqube
helm upgrade --install -n sonarqube sonarqube sonarqube/sonarqube
```


```yaml
kubectl apply -f - << EOF
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: sonarqube
  namespace: sonarqube
  annotations:
    kubernetes.io/ingress.class: caddy
spec:
  rules:
    - host: sonarqube.shubhamtatvamasi.com
      http:
        paths:
        - path: /
          pathType: Prefix
          backend:
            service:
              name: sonarqube-sonarqube
              port:
                number: 9000
EOF
```

get password
```bash
kubectl get secrets sonarqube-sonarqube-monitoring-passcode -n sonarqube -o jsonpath='{.data.SONAR_WEB_SYSTEMPASSCODE}' | base64 -d
```

