Initialising Kubernetes... done

controlplane:~$ kubectl get nodes
NAME           STATUS   ROLES           AGE    VERSION
controlplane   Ready    control-plane   6d1h   v1.32.1
node01         Ready    <none>          6d     v1.32.1
controlplane:~$ kubectl run nginx --image=nginx
pod/nginx created
controlplane:~$ kubectl get pods
NAME    READY   STATUS    RESTARTS   AGE
nginx   1/1     Running   0          18m
controlplane:~$ cat ~/.kube/config
apiVersion: v1
clusters:
- cluster:
    certificate-authority-data: LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSURCVENDQWUyZ0F3SUJBZ0lJTkx4a2N6QnZZVVF3RFFZSktvWklodmNOQVFFTEJRQXdGVEVUTUJFR0ExVUUKQXhNS2EzVmlaWEp1WlhSbGN6QWVGdzB5TlRBMk1UQXdPREl4TVRsYUZ3MHpOVEEyTURnd09ESTJNVGxhTUJVeApFekFSQmdOVkJBTVRDbXQxWW1WeWJtVjBaWE13Z2dFaU1BMEdDU3FHU0liM0RRRUJBUVVBQTRJQkR3QXdnZ0VLCkFvSUJBUUMzT0xrNGwyQ0VURUNWQituWnJLcC9Cemxwb1ZNa0R6VnErdjhhaVZEMXN4RnQ1SUhWM0c0Y0ZaVnMKdUtJTXBLdklha2djOWZ3NFhGWXdqZldPQnZ2U2VORU43c1dkRWk0aDBVOFhSMHpWY3BrdFJ2bHJpVWxWS3ZaQQp5eitmNGZHT1dqOW9WKzR2dkQ4QjJsTDNISE1xQ1ppTHhmNlJUb1hWT3RXTCtScjdaRTFoWE9CamNHcVhMSUc2ClQveFlFQVUyZnR5WTQ0c0lVUEo0SlJXQXhLS2xHQkdhUkxKM3ZPbStXV1l3RFZ5eDQybCtsU2xDOHZYWis0aXAKUHdwOEFDc1JXYldyMVAvR0pKT1Jpc0xoZVk5d0NJaXMyMTB4TGF2WUMvSjV4UldhUTFPY012YVA4OEgxM21DOQpDRTBnaGNSYkdGWHdTQXBkQ2JWVy8vYmlPZmpwQWdNQkFBR2pXVEJYTUE0R0ExVWREd0VCL3dRRUF3SUNwREFQCkJnTlZIUk1CQWY4RUJUQURBUUgvTUIwR0ExVWREZ1FXQkJSNUNIaDhkeGFnQktCanhlVEFCWHFaRWxjVTJ6QVYKQmdOVkhSRUVEakFNZ2dwcmRXSmxjbTVsZEdWek1BMEdDU3FHU0liM0RRRUJDd1VBQTRJQkFRQnplbFVZcnloZwpqdktUYk9icVppZGNHOEcrZmc5UW11SG1BVFoxU21XMmRISUF4aERUS1I3Zkk5L21ZYTh6Z3lOcG95ZWZwYm1DCkdtd1pHNHQvV3ZyY3VVSTBWQWhvVFd6dzdybjBDM0J6QnBCMDFzUzV0R2ViTGc5clBRdWFsRDB1K09lbUZvU1YKZ0lNazVUbEZHYU1IQ0lqVTZLTjlzUHFpa1Zqc1VmK0s2aHF3ajFDNFNidy9EUDlwS0xtRXhFYkJiVEVEdlZvTQoxOVJHL29IMGx2NXNZQ28xMS8xY2pKM2xmcmk3YnQ2Z0F0aUVCQ3p3QjcrQ0p0UlU2VTQrbXIvVjJsU3Bhd2xoCm9ialcvK01HYWc0emc5NW84bC9idnp6THhPVzF6SVE5SjJya1Z2NnJQMzNlaHlTZnZob3JiUU0xWXdsUE4xZmgKQlQySENRbW1Hc0kyCi0tLS0tRU5EIENFUlRJRklDQVRFLS0tLS0K
    server: https://172.30.1.2:6443
  name: kubernetes
contexts:
- context:
    cluster: kubernetes
    user: kubernetes-admin
  name: kubernetes-admin@kubernetes
current-context: kubernetes-admin@kubernetes
kind: Config
preferences: {}
users:
- name: kubernetes-admin
  user:
    client-certificate-data: LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSURLVENDQWhHZ0F3SUJBZ0lJQy9zOElvbW5MTlV3RFFZSktvWklodmNOQVFFTEJRQXdGVEVUTUJFR0ExVUUKQXhNS2EzVmlaWEp1WlhSbGN6QWVGdzB5TlRBMk1UQXdPREl4TVRsYUZ3MHlOakEyTVRBd09ESTJNVGxhTUR3eApIekFkQmdOVkJBb1RGbXQxWW1WaFpHMDZZMngxYzNSbGNpMWhaRzFwYm5NeEdUQVhCZ05WQkFNVEVHdDFZbVZ5CmJtVjBaWE10WVdSdGFXNHdnZ0VpTUEwR0NTcUdTSWIzRFFFQkFRVUFBNElCRHdBd2dnRUtBb0lCQVFEUXk1SE4KbVNzemF1b1NkQkhvd3phdDhmWkJXd2xVUk1HVTRiQzJDRXVvVTFORytKYlB0QjYzcU0zd2RFRnN6dzEvd09rcQpuT05FblQ5OUhiSWdCTk80MEpMdTlOT2RCaTVsakNBQllEMWlodlhocjY0dldHMUdkSCtpTm9KMVk0dE5sTHZTCkhXOXF1WnBrS3RsUHNrQ1dWUnVWemhtWjh1K2FCaWo3K3NZbDRyVlg0Vzd2NUd1UU55cVhBWkx2ZUtsbWw4QVQKWDlzeHBkc1dqK1pVRGF0REpSOTErVXhsaXNPbU95Y0I3UGV1a1M4RmFvK0RtMnEwLzEwMUJ6QUVCeVlhcnN2VgpwalZBcXdpNldraUxOa25vdnlWbHArQmJnNEF6Wnp0YXBmVjVqTEFTWXpvSlY5VGJoQ05hR20zQ1N2N3ZEUUxLCklGOEErZHprcU1saDY0ZFZBZ01CQUFHalZqQlVNQTRHQTFVZER3RUIvd1FFQXdJRm9EQVRCZ05WSFNVRUREQUsKQmdnckJnRUZCUWNEQWpBTUJnTlZIUk1CQWY4RUFqQUFNQjhHQTFVZEl3UVlNQmFBRkhrSWVIeDNGcUFFb0dQRgo1TUFGZXBrU1Z4VGJNQTBHQ1NxR1NJYjNEUUVCQ3dVQUE0SUJBUUNqLzFQbm9EZk5aVkx2Z0t4cmhVZXc3SHNRCkxMWkhaWDVJSXcxRFRHcU9ubWZLZGQrNDFTdXJFd0RXUW1FWXZwdW5ZSnB5VmV3ckNGdWlabWJidDZLM1NySFkKQVY0L2puZlpZc0locWFZaUZSUkRJQzVGQ2FFZXJES1ZTNVA4a2FrTzVnVW84VDR2SEc3ZDZmOUxJOUt1YUlSYwpmaEhqTk15MkVPNGhYS01CTWdLT3hqMFpxeGp1VFUyaFp0bW5oL0VjeCtHa1ptWEtlWmd1UkhkbDV4SmZPakUyCmlJOG9tb1dJZGIrOW9lVUtvYThOZEFOTVRtUVdmS09INitGaDBFWk5XWExIN1ZWTWZwZjk3Nm5hMGVHOHA4WlgKMmlrckRWUVlrZDRUTElxSTBjdUxTK1dqZG43Rng3T2dSeUFXdkhadGhQNlF3U1ptbXJORk5keWZnY3JRCi0tLS0tRU5EIENFUlRJRklDQVRFLS0tLS0K
    client-key-data: LS0tLS1CRUdJTiBSU0EgUFJJVkFURSBLRVktLS0tLQpNSUlFb3dJQkFBS0NBUUVBME11Unpaa3JNMnJxRW5RUjZNTTJyZkgyUVZzSlZFVEJsT0d3dGdoTHFGTlRSdmlXCno3UWV0NmpOOEhSQmJNOE5mOERwS3B6alJKMC9mUjJ5SUFUVHVOQ1M3dlRUblFZdVpZd2dBV0E5WW9iMTRhK3UKTDFodFJuUi9vamFDZFdPTFRaUzcwaDF2YXJtYVpDclpUN0pBbGxVYmxjNFptZkx2bWdZbysvckdKZUsxVitGdQo3K1Jya0RjcWx3R1M3M2lwWnBmQUUxL2JNYVhiRm8vbVZBMnJReVVmZGZsTVpZckRwanNuQWV6M3JwRXZCV3FQCmc1dHF0UDlkTlFjd0JBY21HcTdMMWFZMVFLc0l1bHBJaXpaSjZMOGxaYWZnVzRPQU0yYzdXcVgxZVl5d0VtTTYKQ1ZmVTI0UWpXaHB0d2tyKzd3MEN5aUJmQVBuYzVLakpZZXVIVlFJREFRQUJBb0lCQUJCcDhHeFpQaXdzbTNvWAo1ZENHaUNYa2Y1ZGpzTGdQTDZpa2xWKzZCemlVVkZlZjh6c2d6Y2xpVzg0clZYbFlUWmRkY3ZjR25sY21oWGN3CmZuQkY4TjcyaHBhQ2FLQlBmQlkvamNTTjdFVnlscUhIVGNvckNXd2dmR2drSU4xWmxmbmpWMkNOTDlVVUFpOGQKcnplMHE1OGwwYVZWTG00THl3b3dzY2dkVHJacmw3TGh4RTZoK1hHVVZmYXptQzd5dmUwekJZNVZZVzJmTEpTUwpRNGZka1JOV0xDNktLaGhQdmJNY1BKRnplVHNFSGd1MDU0UmpIckw0UXhUYVpGV3ZtTU56VEppUlg0UjY4UDlvCmVLRUxzNDRkbDBYZDI1TkZ5ZHNBSUFIVFg3QjVsVG55WFV2TVRaMGtZbThrckxKT3RJM1hYbk5iQkdPU3pFWVIKYk5zZ0NBRUNnWUVBOGRZakVPUlFxN2JoQTdCQ1pkNnRyVWwzRnhQQ0F3WlZkUWtVdGI1ZUZFTDJQcUFuYjI5eQpFYlkvMktZdXk3TmIweXlISExqcGdMMzVrOUhqUGFsQkJWUk5mMHVYWUlTMlZqMkUyUUlHOXRrQXJCRFQyaklYCjlGMVlZZHI5bXp2TGJRMUFnb1BzanNHTE9nVk9NREhHZitlczZqWGFHUUJTa0RUT0hXM3l6QkVDZ1lFQTNRWUwKSU03WHVJUmc2RmNxajRYcUpYVlVNMFE5cUZGeUUvcDFPTk9rejJjdFQrZktSMTlZeXp5Ykg1RUNBNEorMkswRAo0bTN4WFBFY2lya2hHdVcxZ21tT25RcjBNWFpFdVNEdlJiaXI2bXkwcW5PVVdaVjUvOThhT21WQTdGWHdyaXlDCmprVlc3aTIvc0xWd09UNFFGS3FQTCtXeE44TVVPZlh1WnZUcjJ3VUNnWUVBcnJUbEZrSHFxWEp2Y2d1Mm5BTlgKY3JWOUREWGcxZkNRY2dGQ2JkMTk5Nk04WTVldGhZcDhYS0ZOMUlTUmorVWQ5QnZaNi8wRjYxVFM1V0FlaXlBbgo4ZUtxTGNqOUxlUVNHWkZOMUx2ckxnOHN0aUZkK3VadmVjQ3BwZC9ma0hLTkRsWWhnV2d1MEI2d0p4VklHL2NKCmtNTmNuc0tTc2JjUzdrekhqbWtzbXhFQ2dZQlFySEVKWTVaSHFrSDQ3RUFEclB4KythbG5JUVJrV0g0TUhzSUUKb1BPcUpGM2NxWjBpbWdHK0JQd1Y5SWJJb3l3TGlITS9oYU93cWUwaUVWcXRCNlZOMlp1TlpMOG5BcVVvOFlXRQpiRmlMczJ2cVAwK3B0eTZWbjJoaVlpemxWcVVIM2dVMVNzZmxIZHUyOHpMb0llZ2FzdnFhbi9za2dGYjBwUGlFCnFlY2d4UUtCZ0FtbHV1anhWaFRLbXlZdytONjUydVJLZVhONjBIdGFGanBlZktnRUU4Tlp2TW9RYms2QkV0T1kKVEN1Q1EwY1h0RWtidW5ta3pXaGxuanU3cTNIMWFQbkVNd2lEQnBxQU5zbWQzUlhKUGNWN0VtQnh1czdJcnl1Zwo4dDVEWnBPWm5kVzIyaDVzejFRZXc4T0ZmOEJoemV3ZjFmb1J5Vzc5K3BSaGRCSjZCYVh5Ci0tLS0tRU5EIFJTQSBQUklWQVRFIEtFWS0tLS0tCg==
controlplane:~$ kubectl config view
apiVersion: v1
clusters:
- cluster:
    certificate-authority-data: DATA+OMITTED
    server: https://172.30.1.2:6443
  name: kubernetes
contexts:
- context:
    cluster: kubernetes
    user: kubernetes-admin
  name: kubernetes-admin@kubernetes
current-context: kubernetes-admin@kubernetes
kind: Config
preferences: {}
users:
- name: kubernetes-admin
  user:
    client-certificate-data: DATA+OMITTED
    client-key-data: DATA+OMITTED
controlplane:~$ kubectl config get-context
error: unknown command "get-context"
See 'kubectl config -h' for help and examples
controlplane:~$ kubectl config get-contexts
CURRENT   NAME                          CLUSTER      AUTHINFO           NAMESPACE
*         kubernetes-admin@kubernetes   kubernetes   kubernetes-admin   
controlplane:~$ 



kubectl get csr snj -o jsonpath='{.status.certificate}' | base64 --decode > snj.crt
------------------------------------------------


Initialising Kubernetes... done

controlplane:~$ openssl genrsa -out snj.key 2048
controlplane:~$ openssl req -new -key snj.key -out snj.csr -subj "/CN=snj/O=group1"
controlplane:~$ ls
filesystem  snj.csr  snj.key

controlplane:~$ cat snj.csr | base64 | tr -d '\n'
LS0tLS1CRUdJTiBDRVJUSUZJQ0FURSBSRVFVRVNULS0tLS0KTUlJQ1pEQ0NBVXdDQVFBd0h6RU1NQW9HQTFVRUF3d0RjMjVxTVE4d0RRWURWUVFLREFabmNtOTFjREV3Z2dFaQpNQTBHQ1NxR1NJYjNEUUVCQVFVQUE0SUJEd0F3Z2dFS0FvSUJBUUNQTDZCVDBXSkxITWZuOTJ3NlZ6c1h0OGFJClgvWEdJQ2tGMmt1RnArNTBtTmVyUU1Wb3ROQTFhdVB3QUk3Q0c2MEU2OE1Ed0RvU3c2RzZUYWdUZWt5Qm12TjgKZitHMExBYndRQUZDc1htci9BbnMxT1RvTlg4eHlNMko4MWdZRnRkbi9wZ3d2eXRZZVlTOVFEMFZ4UlRWQkI0TwpJekhGYjA1U3BSbm93ZmprTVEzdlhQaGh2bkMwcGs4L3NSY0lKSC8rL0pkNW5SRWNqMkZVOGkwRERmR2crR2Q2CjBKVStKSnltSkFudG5aTlcva0xEVVFpMUNsRVB4MnFXakd2TEFha1NuWFZYNnZHNVFnT2txdzZNTjVpbDkwMkcKdUhROWIyMWRteEkrOHlhVk9ET0FRbm96WmRHbUxTbFJaNXA3N3JlOWtNMDhkcVJKVlFqRC9iRDBuMmU3QWdNQgpBQUdnQURBTkJna3Foa2lHOXcwQkFRc0ZBQU9DQVFFQU1RYTFjVVZSU0FyV2l4Wk9jL093UlI4REZVbjVOTUZRCmYwZWFPT2NCU2cwVmF6cWxkbGlrLytRN3FMTWRDVjhURjcxWElpNStXTHVjVkY1MWRSWVNLNzREbW0xTklHTWUKcDZFU1pkMGFGcFBDVm1RMTFPY2pYL1ZlNXdBRld3azNBSEV1TkMxdkd1eGtNdlZUMEt4SWlDSzZOK1ZsSUQzMgp4Y1BCRTJ6K081cnpIRjY4dUtGbHVIY2ZFUUhEVGRxcFc4Z2dmNGN0SXVhcEZIYjZ6WXh4c1NYYm5aQ3NZVkFlCjVyb0NPZENFcEVVTmk0bEFNa1hlRGhNRkttSWJFYVBLeUROY1dTVVFwSTN1U0pPVGZGZkxKY2g1QjQ0a3RVWVQKcU5aUlF6SjNPL2lZTm96OTdocGtOZnZhQThNbUJ4bURXYWEwR3pDa1gxK2ludFhxY2pDUmdBPT0KLS0tLS1FTkQgQ0VSVElGSUNBVEUgUkVRVUVTVC0tLS0tCg==
controlplane:~$ 
controlplane:~$ vi csr.yaml
controlplane:~$ vi csr.yaml
controlplane:~$ vi csr.yaml
controlplane:~$ kubectl apply -f csr.yaml  
certificatesigningrequest.certificates.k8s.io/snj created
controlplane:~$ kubectl certificate approve snj
certificatesigningrequest.certificates.k8s.io/snj approved
controlplane:~$ kubectl get csr snj -o jsonpath='{.status.certificate}' | base64 --decode > snj.crt
controlplane:~$ ls
csr.yaml  filesys

------------------------------------------------------------------------------------------------------------------

Section 3 - YAML, POD, POD lifecycle, init container, sidecar container

  POD lifecycle - pending 


  Initialising Kubernetes... done

controlplane:~$ kubectl get nodes
NAME           STATUS   ROLES           AGE     VERSION
controlplane   Ready    control-plane   6d15h   v1.32.1
node01         Ready    <none>          6d14h   v1.32.1
controlplane:~$ kubectl get nodes node01 -oyaml | grep CIDR
  podCIDR: 192.168.1.0/24
  podCIDRs:
controlplane:~$ 


controlplane:~$ kubectl get ns  
NAME                 STATUS   AGE
default              Active   6d15h
kube-node-lease      Active   6d15h
kube-public          Active   6d15h
kube-system          Active   6d15h
local-path-storage   Active   6d15h
controlplane:~$ kubectl create ns bootcamp
namespace/bootcamp created
controlplane:~$ kubectl get pods          
No resources found in default namespace.
controlplane:~$ kubectl run snj --image snj
pod/snj created
controlplane:~$ kubectl describe pod       
Name:             snj
Namespace:        default
Priority:         0
Service Account:  default
Node:             node01/172.30.2.2
Start Time:       Mon, 16 Jun 2025 23:45:08 +0000
Labels:           run=snj
Annotations:      cni.projectcalico.org/containerID: 80895b8835990e27eace8176579fc5e1c3ebb1883383f60ae98ba9b5038bc3a5
                  cni.projectcalico.org/podIP: 192.168.1.4/32
                  cni.projectcalico.org/podIPs: 192.168.1.4/32
Status:           Pending
IP:               192.168.1.4
IPs:
  IP:  192.168.1.4
Containers:
  snj:
    Container ID:   
    Image:          snj
    Image ID:       
    Port:           <none>
    Host Port:      <none>
    State:          Waiting
      Reason:       ImagePullBackOff
    Ready:          False
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-t95v5 (ro)
Conditions:
  Type                        Status
  PodReadyToStartContainers   True 
  Initialized                 True 
  Ready                       False 
  ContainersReady             False 
  PodScheduled                True 
Volumes:
  kube-api-access-t95v5:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type     Reason     Age                   From               Message
  ----     ------     ----                  ----               -------
  Normal   Scheduled  4m30s                 default-scheduler  Successfully assigned default/snj to node01
  Normal   Pulling    68s (x5 over 4m30s)   kubelet            Pulling image "snj"
  Warning  Failed     62s (x5 over 4m22s)   kubelet            Failed to pull image "snj": failed to pull and unpack image "docker.io/library/snj:latest": failed to resolve reference "docker.io/library/snj:latest": pull access denied, repository does not exist or may require authorization: server message: insufficient_scope: authorization failed
  Warning  Failed     62s (x5 over 4m22s)   kubelet            Error: ErrImagePull
  Normal   BackOff    10s (x14 over 4m21s)  kubelet            Back-off pulling image "snj"
  Warning  Failed     10s (x14 over 4m21s)  kubelet            Error: ImagePullBackOff
controlplane:~$ kubectl get pods -owide
NAME   READY   STATUS             RESTARTS   AGE   IP            NODE     NOMINATED NODE   READINESS GATES
snj    0/1     ImagePullBackOff   0          6m    192.168.1.4   node01   <none>           <none>
controlplane:~$ 

====================================
SECTION 4-
SideCar container , QOS, PDB(Pod discruption budget), Request Limit