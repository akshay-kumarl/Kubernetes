# Secrets

General folder structure 
deployment.yaml
service.yaml
hpa.yaml [optional]
secret.yaml

### Deployment
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app-deployment
  namespace: default
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-app-container
        image: nginx  # Replace with your application image
        ports:
        - containerPort: 80
        env:
        - name: DB_USERNAME
          valueFrom:
            secretKeyRef:
              name: db-secret
              key: db-username
        - name: DB_PASSWORD
          valueFrom:
            secretKeyRef:
              name: db-secret
              key: db-password
```

---

### Service

```
apiVersion: v1
kind: Service
metadata:
  name: my-app-service
  namespace: default
spec:
  selector:
    app: my-app
  ports:
    - name: http
      protocol: TCP
      port: 80          # Port that the service will expose
      targetPort: 80    # Port that the container listens on
  type: NodePort       # Change to LoadBalancer or NodePort if needed
```

---

### Secret

```
apiVersion: v1
kind: Secret
metadata:
  name: db-secret
  namespace: default
type: Opaque
data:
  db-username: bXlVc2VybmFtZQ==  # base64 encoded value of "myUsername"
  db-password: cGFzc3dvcmQ=      # base64 encoded value of "password"
```

---

base64 encoded notes
```
echo -n 'abcdefg' | base64 
```
to decode base64 
```
echo 'YWJjZGVmZw==' | base64 --decode 
```
