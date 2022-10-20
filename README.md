# VMware Tanzu


![image](https://user-images.githubusercontent.com/79700810/196868448-b8fb6d65-8ae7-4f40-a5a9-4a3523782995.png)


![image](https://user-images.githubusercontent.com/79700810/196868614-db241d31-bf55-48bb-aa67-7d428f2dfa3d.png)


![image](https://user-images.githubusercontent.com/79700810/196870585-69d1f2f0-03f8-49ba-8fae-6440b1543f1e.png)

```
kubectl-vsphere login --insecure-skip-tls-verify --server=10.174.72.209
```

![image](https://user-images.githubusercontent.com/79700810/196872137-33d381b0-d489-4df2-a5db-ed72cbafdde0.png)


kubectl config get-contexts

kubectl config use-context sk8s1

![image](https://user-images.githubusercontent.com/79700810/196872216-782ec69c-1d04-4608-84c0-d8113239d5cd.png)


tkgs-cluster-1.yaml

```yaml
apiVersion: run.tanzu.vmware.com/v1alpha2
kind: TanzuKubernetesCluster
metadata:
  name: tkgs-cluster-1
  namespace: sk8s1
```

![image](https://user-images.githubusercontent.com/79700810/196872419-19ffc59c-4c57-447b-a268-69efcd6515a8.png)


```
kubectl get virtualmachineclassbindings
```


```yaml
spec:
  topology:
    controlPlane:
      replicas: 1
      vmClass: best-effort-xsmall      
```

![image](https://user-images.githubusercontent.com/79700810/196873145-b560f7f8-ee6c-4dcd-8a3b-8f9ddd9fd1a6.png)


```
kubectl describe storageclasses
```

```yaml
storageClass: kubernetes-gold-storage-policy
      volumes:
        - name: etcd
          mountPath: /var/lib/etcd
          capacity:
            storage: 4Gi
```

![image](https://user-images.githubusercontent.com/79700810/196873497-0fd8b866-c811-4e04-ac79-cbeb1f7c7cad.png)


```yaml
apiVersion: run.tanzu.vmware.com/v1alpha2
kind: TanzuKubernetesCluster
metadata:
  name: tkgs-cluster-1
  namespace: sk8s1
spec:
  topology:
    controlPlane:
      replicas: 1
      vmClass: best-effort-xsmall 
      storageClass: kubernetes-gold-storage-policy
      volumes:
        - name: etcd
          mountPath: /var/lib/etcd
          capacity:
            storage: 4Gi
      tkr:
        reference:
          name: v1.21.6---vmware.1-tkg.1.b3d708a
    nodePools:
    - name: worker-nodepool-a1
      replicas: 2
      vmClass: best-effort-xsmall
      storageClass: kubernetes-gold-storage-policy
      volumes:
        - name: containerd
          mountPath: /var/lib/containerd
          capacity:
            storage: 16Gi
      tkr:
        reference:
          name: v1.21.6---vmware.1-tkg.1.b3d708a
     - name: worker-nodepool-a2
       replicas: 2
       vmClass: best-effort-xsmall
       storageClass: kubernetes-gold-storage-policy
       tkr:
         reference:
           name: v1.21.6---vmware.1-tkg.1.b3d708a
  settings:
    storage:
      defaultClass: kubernetes-gold-storage-policy
```
