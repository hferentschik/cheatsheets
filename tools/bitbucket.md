---
title: Gitlab
category: tools
layout: 2017/sheet
intro: |
  How to get BitBucket running on Kubernetes
---

### Installation


```yaml
apiVersion: v1
kind: Secret
metadata:
  name: bitbucket-postgres
type: Opaque
data:
  username: YWRtaW4=
  password: YWRtaW4=
  postgres_db: Yml0YnVja2V0
---
kind: PersistentVolumeClaim
apiVersion: v1
metadata:
  name: postgres-pv-claim
  labels:
    app: postgres
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 5Gi
---
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  name: postgres
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: postgres
    spec:
      containers:
        - name: postgres
          image: postgres:10.4
          imagePullPolicy: "IfNotPresent"
          ports:
            - containerPort: 5432
          env:
          - name: POSTGRES_DB
            valueFrom:
              secretKeyRef:
                name: bitbucket-postgres
                key: postgres_db
          - name: POSTGRES_USER
            valueFrom:
              secretKeyRef:
                name: bitbucket-postgres
                key: username
          - name: POSTGRES_PASSWORD
            valueFrom:
              secretKeyRef:
                name: bitbucket-postgres
                key: password
          volumeMounts:
            - mountPath: /var/lib/postgresql/data
              name: postgredb
              subPath: postgres
      volumes:
        - name: postgredb
          persistentVolumeClaim:
            claimName: postgres-pv-claim
---
apiVersion: v1
kind: Service
metadata:
  name: postgres
spec:
  selector:
    app: postgres
  ports:
  - protocol: TCP
    port: 5432
    targetPort: 5432
---
kind: PersistentVolumeClaim
apiVersion: v1
metadata:
  name: bitbucket-pv-claim
  labels:
    app: bitbucket
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 5Gi
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: bitbucket
  labels:
    app: bitbucket
spec:
  replicas: 1
  selector:
    matchLabels:
      app: bitbucket
  template:
    metadata:
      labels:
        app: bitbucket
    spec:
      containers:
      - name: bitbucket
        image: atlassian/bitbucket-server
        ports:
        - containerPort: 7990
          name: bitbucket-http
        - containerPort: 22
          name: bitbucket-ssh
        volumeMounts:
        - mountPath: /var/atlassian/application-data/bitbucket
          name: bitbucket-data
        env:
        - name: SERVER_PROXY_NAME
          value: ""
      volumes:
        - name: bitbucket-data
          persistentVolumeClaim:
            claimName: bitbucket-pv-claim
---
kind: Service
apiVersion: v1
metadata:
  name: bitbucket
spec:
  selector:
    app: bitbucket
  ports:
  - name: bitbucket-http
    port: 7990
    targetPort: bitbucket-http
  - name: bitbucket-ssh
    port: 2222
    targetPort: bitbucket-ssh
  type: LoadBalancer
```

```bash
> kubectl apply -f bitbucket.yaml
```

### Links

* [BitBucket on Kube](https://medium.com/@jmarhee/running-atlassian-bitbucket-server-on-kubernetes-e3f13779ae36)






