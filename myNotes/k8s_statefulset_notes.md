### Working Example with Persistent Volumes
Consider the following StatefulSet, which provisions a three-node Redis cluster. Each Redis node has
its own unique identity and persistent storage.

```
apiVersion: apps/v1
kind: StatefulSet
metadata:
 name: redis
spec:
 serviceName: "redis"
 replicas: 3
 selector:
 matchLabels:
 app: redis
 template:
 metadata:
 labels:
 app: redis
 spec:
 containers:
 - name: redis
 image: redis:6.0
 ports:
 - containerPort: 6379
 name: redis
 volumeMounts:
 - name: redis-storage
 mountPath: /data
 volumeClaimTemplates:
 - metadata:
 name: redis-storage
 spec:
 accessModes: [ "ReadWriteOnce" ]
 resources:
 requests:
 storage: 2Gi
```

---

### StatefulSet Configuration
Below is an example of a basic StatefulSet YAML configuration for a MySQL application:

```
apiVersion: apps/v1
kind: StatefulSet
metadata:
 name: mysql
spec:
 serviceName: "mysql"
 replicas: 3
 selector:
 matchLabels:
 app: mysql
 template:
 metadata:
 labels:
 app: mysql
 spec:
 containers:
 - name: mysql
 image: mysql:5.7
 ports:
 - containerPort: 3306
 name: mysql
 volumeMounts:
 - name: mysql-persistent-storage
 mountPath: /var/lib/mysql
 volumeClaimTemplates:
 - metadata:
name: mysql-persistent-storage
 spec:
 accessModes: [ "ReadWriteOnce" ]
 resources:
 requests:
 storage: 1Gi
```

