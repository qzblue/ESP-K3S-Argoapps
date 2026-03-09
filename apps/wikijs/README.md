# Wiki.js on K3S (Argo CD)

此目录用于通过 Argo CD 在 K3S 部署 Wiki.js，连接外部 MySQL。

当前配置：
- 域名：`wiki.esp.edu.kg`
- 数据库主机：`10.32.65.22:3306`
- 数据库名：`wikijs`
- 数据库用户：`wikijs`
- PVC：`10Gi`（使用默认 StorageClass）

## 1. 提交并推送

```powershell
git add apps/wikijs
git commit -m "feat(wikijs): deploy wikijs by argocd"
git push origin main
```

## 2. 在集群创建 Argo CD Application

```powershell
kubectl apply -f apps/wikijs/argocd-application.yaml
```

确认 Argo CD 已同步：

```powershell
kubectl get application -n argocd wikijs-app
kubectl describe application -n argocd wikijs-app
```

## 3. DNS 配置

将 `wiki.esp.edu.kg` 的 A 记录指向 K3S Ingress 对外 IP（Traefik 暴露地址）。

## 4. MySQL 授权（在 10.32.65.22 执行）

```sql
CREATE DATABASE IF NOT EXISTS wikijs CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
CREATE USER IF NOT EXISTS 'wikijs'@'%' IDENTIFIED BY 'sJEY82wEeXKeic6w';
GRANT ALL PRIVILEGES ON wikijs.* TO 'wikijs'@'%';
FLUSH PRIVILEGES;
```

## 5. 验证

```powershell
kubectl get pods -n wikijs -o wide
kubectl get svc -n wikijs
kubectl get ingress -n wikijs
kubectl logs -n wikijs deploy/wikijs --tail=100
```

浏览器访问：`http://wiki.esp.edu.kg`

首次访问按向导完成管理员初始化即可。
