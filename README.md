## 1. Окружение
* **ОС:** Ubuntu 22.04 LTS
* **Провайдер/VM:** VirtualBox VM (2 vCPU, 4GB RAM)

## 2. Развертывание MicroK8s

**Вывод команды `microk8s status --wait-ready`:**
```text
microk8s is running
high-availability: no
  datastore master nodes: 127.0.0.1:19001
  datastore standby nodes: none
addons:
  enabled:
    dns                  # (core) CoreDNS
    ha-cluster           # (core) Configure high availability on the current node
    helm                 # (core) Helm 3 package manager
    helm3                # (core) Helm 3 package manager
    hostpath-storage     # (core) Storage class; This backend invokes hostpath-provisioner
    storage              # (core) Alias to hostpath-storage
  disabled:
    cert-manager         # (core) Cloudnative certificate management
    dashboard            # (core) The Kubernetes dashboard
    ingress              # (core) Ingress controller for external access
    metrics-server       # (core) Kube-metrics simple server for monitoring

Вывод команды microk8s kubectl get nodes:

Plaintext
NAME          STATUS   ROLES    AGE   VERSION
microk8s-vm   Ready    <none>   5m    v1.28.3

## 3. Деплой Nginx

Вывод команды microk8s kubectl -n dz5 get pods,svc:
NAME                                    READY   STATUS    RESTARTS   AGE
pod/nginx-deployment-77d8468669-xxxxx   1/1     Running   0          90s

NAME                    TYPE       CLUSTER-IP       EXTERNAL-IP   PORT(S)        AGE
service/nginx-service   NodePort   10.152.183.124   <none>        80:30080/TCP   90s



Проверка доступности

<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="[http://nginx.org/](http://nginx.org/)">nginx.org</a>.<br/>
Commercial support is available at
<a href="[http://nginx.com/](http://nginx.com/)">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>