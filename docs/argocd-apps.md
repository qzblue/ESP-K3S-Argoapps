# Argo CD App 操作文档

本文档用于统一管理本仓库的 Argo CD `Application` 操作流程。

## 1. 在 manager 找到仓库路径

你之前看到的：

```bash
cd /path/to/ESP-K3S-Argoapps
```

`/path/to/...` 是占位符。先在 manager 上执行：

```bash
find / -type d -name ESP-K3S-Argoapps 2>/dev/null
```

如果返回例如：

```text
/home/ubuntu/ESP-K3S-Argoapps
```

那就执行：

```bash
cd /home/ubuntu/ESP-K3S-Argoapps
```

## 2. 通用部署流程（所有 app 通用）

```bash
cd <你的仓库实际路径>
git pull
kubectl apply -f <app目录>/argocd-application.yaml
kubectl get application -n argocd
kubectl describe application -n argocd <application-name>
```

## 3. Wiki.js 专用流程

当前 Application 文件：

`apps/wikijs/argocd-application.yaml`

部署命令：

```bash
cd <你的仓库实际路径>
git pull
kubectl apply -f apps/wikijs/argocd-application.yaml
kubectl get application -n argocd wikijs-app
kubectl get pods -n wikijs -o wide
kubectl get ingress -n wikijs
kubectl logs -n wikijs deploy/wikijs --tail=100
```

## 4. 常用排错

查看 Argo CD 同步状态：

```bash
kubectl get application -n argocd
kubectl describe application -n argocd wikijs-app
```

如果资源没有创建，重点看：
- `spec.source.path` 是否存在（当前为 `apps/wikijs`）
- `repoURL` 是否和你实际仓库一致
- Argo CD 是否有权限访问目标集群

如果 Pod 启不来，重点看：

```bash
kubectl describe pod -n wikijs -l app=wikijs
kubectl logs -n wikijs deploy/wikijs --tail=200
```

## 5. 域名与数据库前提（Wiki.js）

- DNS A 记录：`wiki.esp.edu.kg` -> K3S Ingress 对外 IP
- MySQL 地址：`10.32.65.22:3306`
- DB：`wikijs`
- 用户：`wikijs`

