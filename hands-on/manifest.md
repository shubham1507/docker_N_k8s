# 📁 k8s-hands-on-tasks

## 1. pod-multi-container-sidecar.yaml
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-sidecar
spec:
  volumes:
  - name: shared-logs
    emptyDir: {}
  containers:
  - name: nginx
    image: nginx
    volumeMounts:
    - name: shared-logs
      mountPath: /var/log/nginx
  - name: log-tailer
    image: busybox
    command: ['sh', '-c', 'tail -f /var/log/nginx/access.log']
    volumeMounts:
    - name: shared-logs
      mountPath: /var/log/nginx
```

## 2. pod-init-wait-for-url.yaml
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: wait-for-google
spec:
  initContainers:
  - name: wait-google
    image: busybox
    command: ['sh', '-c', 'until wget -q --spider http://google.com; do echo waiting; sleep 2; done;']
  containers:
  - name: main
    image: busybox
    command: ['sh', '-c', 'echo App started && sleep 3600']
```

## 3. pod-init-download-to-nginx.yaml
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: download-and-serve
spec:
  volumes:
  - name: html-data
    emptyDir: {}
  initContainers:
  - name: downloader
    image: busybox
    command: ['sh', '-c', 'wget -O /usr/share/nginx/html/index.html http://example.com']
    volumeMounts:
    - name: html-data
      mountPath: /usr/share/nginx/html
  containers:
  - name: nginx
    image: nginx
    volumeMounts:
    - name: html-data
      mountPath: /usr/share/nginx/html
```

## 4. pod-crashloop-debug.yaml
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: crashpod
spec:
  containers:
  - name: crash-container
    image: busybox
    command: ['sh', '-c', 'exit 1']
```

## 5. configmap-env.yaml
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
  namespace: default
data:
  ENV: "prod"
  LOG_LEVEL: "debug"
---
apiVersion: v1
kind: Pod
metadata:
  name: app-env
spec:
  containers:
  - name: busybox
    image: busybox
    command: ['sh', '-c', 'env && sleep 3600']
    envFrom:
    - configMapRef:
        name: app-config
```

## 6. pod-command-args.yaml
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: cmd-args-pod
spec:
  containers:
  - name: echoer
    image: busybox
    command: ['sh', '-c']
    args: ['echo Hello Kubernetes && sleep 3600']
```

## 7. pod-security-context.yaml
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: secure-pod
spec:
  securityContext:
    runAsUser: 1000
    runAsGroup: 3000
    fsGroup: 2000
  containers:
  - name: secure-container
    image: busybox
    command: ['sh', '-c', 'id && sleep 3600']
    securityContext:
      readOnlyRootFilesystem: true

