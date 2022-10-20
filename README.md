# VMware Tanzu


![image](https://user-images.githubusercontent.com/79700810/196868448-b8fb6d65-8ae7-4f40-a5a9-4a3523782995.png)


![image](https://user-images.githubusercontent.com/79700810/196868614-db241d31-bf55-48bb-aa67-7d428f2dfa3d.png)


![image](https://user-images.githubusercontent.com/79700810/196870585-69d1f2f0-03f8-49ba-8fae-6440b1543f1e.png)

```
kubectl-vsphere login --insecure-skip-tls-verify --server=10.174.72.209
```

![image](https://user-images.githubusercontent.com/79700810/196872137-33d381b0-d489-4df2-a5db-ed72cbafdde0.png)

``
kubectl config get-contexts
kubectl config use-context sk8s1
```

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


```
kubectl get tanzukubernetesreleases
```


```yaml
      tkr:
        reference:
          name: v1.21.6---vmware.1-tkg.1.b3d708a
```

![image](https://user-images.githubusercontent.com/79700810/196876905-6993504b-d7a0-4ac4-bb04-36d66e8d1d04.png)


```yaml
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
```

![image](https://user-images.githubusercontent.com/79700810/196877110-1d8ab9e0-a9d6-4188-9d27-1458b9d1e5c9.png)


```yaml

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


![image](https://user-images.githubusercontent.com/79700810/196877528-f549b85a-8062-4b0c-9c9b-2db9580930cb.png)



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

```
kubectl.exe apply -f C:\TKG\yaml\tkgs-cluster-1.yaml
```

![image](https://user-images.githubusercontent.com/79700810/196877695-3f1f33f4-6104-4f9a-b22b-bfb94893b9c3.png)


```
kubectl get tanzukubernetesclusters
```


![image](https://user-images.githubusercontent.com/79700810/196880140-d178ce5e-8698-41f1-ab76-e18839a38526.png)


```
kubectl-vsphere login --insecure-skip-tls-verify --server=10.174.72.209 --tanzu-kubernetes-cluster-name tkgs-cluster-1 --tanzu-kubernetes-cluster-namespace sk8s1
```

![image](https://user-images.githubusercontent.com/79700810/196880480-5f700bd5-6dd7-4b10-be43-d635118fe949.png)

```
kubectl config use-context tkgs-cluster-1
```

![image](https://user-images.githubusercontent.com/79700810/196880820-05c410d6-5db3-4dbd-906c-6c9bbbe6c6b5.png)


```
kubectl run nginx --image=nginx
kubectl get pods
```

![image](https://user-images.githubusercontent.com/79700810/196881329-55b9b756-eb17-4c1e-91f9-e6efd672db8b.png)


```
kubectl expose pod nginx --port=80 --target-port=80 --name nginx-lb --type=LoadBalancer
kubectl get services
```

![image](https://user-images.githubusercontent.com/79700810/196881611-6a7d682e-e68c-410e-9a10-485ab8a04e4f.png)



![image](https://user-images.githubusercontent.com/79700810/196881773-7edfad91-ca6b-4ecb-bc10-749c93b4fe14.png)


