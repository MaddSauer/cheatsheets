# kube-virt

## troubleshooting 
i case of the getting started process some pvc are not 'finish' e.g. no upload has procced. then unused pv / pvc hanging around, and uselessp pods are running.

If you try do delete pod, PV or PVC it will be reconiled, so this will not work.

to clean this checkout 
```bash
kubectl get datavolume.cdi.kubevirt.io
NAME         PHASE       PROGRESS   RESTARTS   AGE
upload-pvc   Succeeded   N/A                   6d23h
fedora-33-qcow ...

```

and delete unneeded configs
```bash
kubectl delete datavolume.cdi.kubevirt.io/fedora-33-qcow
```
