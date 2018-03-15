# persistent volume キャパシティ順にソート
```
kubectl get pv --sort-by=.spec.capacity.storage >> /tmp/pv_size
```

# test_deployのレプリカ数を5に変更
```
kubectl scale deploy test_deploy --replicas 5
```

# nslookup service(KUBEDNS_ADDRは必要なら指定する resolv.confとかに書かれていたりkubernetes cluster内から確認する場合には不要？)
```
nslookup service_name.default.svc.cluster.local KUBEDNS_ADDR
```

# nslookup pod (ipは '-' でつなぐ必要がある)
```
nslookup pod-ip-address.namespace_name.pod.cluster.local KUBEDNS_ADDR
```

# logsの保存
```
kubectl logs POD_NAME >> /tmp/hoge.log
```

# etcd snapshota
```
ETCDCTL_API=3 etcdctl --endpoints https://127.0.0.1:2379 snapshot save etcd-snapshot.db --cert="etcd-client.crt" --key="etcd-client.key" --cacert="ca.crt"
ETCDCTL_API=3 etcdctl --endpoints http://127.0.0.1:2379 snapshot save snapshot.db
```

# nmodeにlabelを付与
```
kubectl label nodes node_name disktype=ssd
```


# 特定のlabelがついたnodeの確認
```
kubectl get node -l disktype=ssd
```

# secret作成
```
kubectl create secret generic test-secret --from-literal=password=hogehoge
kubectl create secret generic test-secret --from-literal=username=hogehoge
```

# cpuのload順位並べる
```
kubectl get pod --show-labels
kubectl get pod -l name=cpu-loader
kubectl top pod -l name=cpu-loader
```

# servcie紐付いているpods
```
kubectl get svc -o wide
kubectl get pod -l SELECTOR
```

# drain
```
kubectl drain NODE_NAME --ignore-daemonsets --force
```

## --delete-local-data localにデータを書いているやつはこのオプションも必要っぽい

# scheduleから外したnodeを元に戻す
```
kubectl uncordon NODE_NAME
```

# namespace 作成
```
kubectl create namespace test-namespace
```
