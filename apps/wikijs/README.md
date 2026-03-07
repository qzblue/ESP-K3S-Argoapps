部署说明 — Wiki.js

此目录包含用于在 K3S 集群通过 ArgoCD 部署 Wiki.js 的 Kubernetes 清单。

要点：
- 使用 MySQL 外部数据库（你提供的：10.32.65.22/wikijs/wikijs）
- 不启用 HTTPS/TLS（内部访问）
- 使用集群默认 StorageClass 创建 PVC（10Gi）
- ArgoCD Application 已包含，默认为自动同步

使用方法（在本地 Git 仓库中执行）：

```powershell
# 将更改提交并推送到远端仓库
git add apps/wikijs
git commit -m "feat(wikijs): add manifests"
git push origin main
```

部署后检查：

```powershell
kubectl get pods -n wikijs
kubectl get svc -n wikijs
kubectl get ingress -n wikijs
kubectl logs -n wikijs -l app=wikijs
```

若 Wiki.js 无法启动或无法连接数据库，请确认 MySQL 可达并且凭证正确。
