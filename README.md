监控相关
===

### Prometheus

Prometheus + kube-stat-metrics + node_export

kube-stat-metrics 镜像版本依赖k8scluster的版本。  
例子k8s cluster是1.10 需要用kube-stat-metrics:v1.5    
具体参考：https://github.com/kubernetes/kube-state-metrics/tree/release-1.5