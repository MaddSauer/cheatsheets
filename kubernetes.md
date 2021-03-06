# kubectl cheatsheet

https://kubernetes.io/docs/reference/kubectl/cheatsheet/

setup autocomplete in bash, bash-completion package should be installed first.

```
source <(kubectl completion bash)
```

# Access Control

https://github.com/kubernetes/dashboard/wiki/Access-control

# Access Dashboard

https://github.com/kubernetes/dashboard/wiki/Accessing-Dashboard---1.7.X-and-above

```
kubectl proxy
```

http://localhost:8001/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy/

# Authorization

https://github.com/oursky/kubernetes-github-authn

```
kubectl create namespace project1
kubectl create rolebinding johndoe-admin-binding --clusterrole=admin --user=johndoe --namespace=project1
```

```
kubectl create clusterrolebinding alex-admin-binding --clusterrole=cluster-admin --user=alex
```

# Troubleshooting

## terminiation of a namespaces which stuck in "Terminating..."

```bash
kubectl proxy &
NS=my-namespace
kubectl get ns $NS -o json | sed '/            "kubernetes"/d' |curl -k -H "Content-Type: application/json" -X PUT --data-binary @/dev/stdin http://127.0.0.1:8001/api/v1/namespaces/$NS/finalize

# fg to take back to forground and terminate proxy with ctrl-c

```

##  Get really all resources with kubectl w/o any plugins:
```
kubectl api-resources --verbs=list --namespaced -o name | xargs -n 1 kubectl get --show-kind --ignore-not-found -n $NAMESPACE_NAME
```
