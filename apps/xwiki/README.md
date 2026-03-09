# XWiki 18.1.0 on K3S (Argo CD)

此目录用于通过 Argo CD 在 K3S 部署 XWiki 18.1.0，并连接外部 MySQL。

当前配置：
- 域名：`xwiki.esp.edu.kg`
- 数据库主机：`10.32.65.22:3306`
- 数据库名：`xwiki`
- 数据库用户：`xwiki`
- PVC：`20Gi`

## 1. 提交并推送

```powershell
git add apps/xwiki
git commit -m "feat(xwiki): deploy xwiki 18.1.0 by argocd"
git push origin main
```

## 2. 在集群创建 Argo CD Application

```powershell
kubectl apply -f apps/xwiki/argocd-application.yaml
```

## 3. 验证

```powershell
kubectl get application -n argocd xwiki-app
kubectl get pods -n xwiki -o wide
kubectl get svc -n xwiki
kubectl get ingress -n xwiki
kubectl logs -n xwiki deploy/xwiki --tail=200
```

浏览器访问：`http://xwiki.esp.edu.kg/xwiki/`
