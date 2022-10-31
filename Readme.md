-- Docker Swarm
╭─   FormacaoDevOps 
╰─ kubectl get nodes
NAME             STATUS   ROLES           AGE     VERSION
docker-desktop   Ready    control-plane   3m47s   v1.25.2

**Criando Pods

    FormacaoDevOps  on   eduDevOps 
╰─ kubectl run nginx-pod --image=nginx:latest                                               ─╯
pod/nginx-pod created
╰─ kubectl get pods                                                                         ─╯
NAME        READY   STATUS    RESTARTS   AGE
nginx-pod   1/1     Running   0          77s
╰─ kubectl get pods --watch                                                                 ─╯
NAME        READY   STATUS    RESTARTS   AGE
nginx-pod   1/1     Running   0          112s
╰─ kubectl describe pod nginx-pod                                                           ─╯
Name:             nginx-pod
Namespace:        default
Priority:         0
Service Account:  default
Node:             docker-desktop/192.168.65.4
Start Time:       Fri, 28 Oct 2022 17:21:47 -0300
Labels:           run=nginx-pod
Annotations:      <none>
Status:           Running
IP:               10.1.0.6

** Editando o Pod
    FormacaoDevOps  on   eduDevOps 
╰─ kubectl edit pod nginx-pod

**Aplicando o arquivo de definição
    FormacaoDevOps  on   eduDevOps 
╰─ kubectl apply -f primeiro-pod.yaml
** Removendo um POD
╭─    FormacaoDevOps/kubernetes  on   eduDevOps 
╰─ kubectl delete -f primeiro-pod.yaml                                                      ─╯
pod "primeiro-pod-declarativo" deleted

** Executando o Pod
╭─    FormacaoDevOps/PortalNoticias  on   eduDevOps !2 ?1 
╰─ kubectl exec -it portal-noticias -- bash

**Delete Pods
FormacaoDevOps/PortalNoticias  on   eduDevOps !1 ?5 
╰─ kubectl delete pod --

** Setup Services