apiVersion: v1
kind: Service
metadata:
  name: svc-cluster
spec:
  type: ClusterIP
  ports:
  - port: 80
    port: 433
  selector:
    app: wordpress
