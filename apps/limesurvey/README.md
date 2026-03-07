# LimeSurvey on K3s (Argo CD)

This directory deploys LimeSurvey with plain Kubernetes manifests managed by Argo CD.

## Version Lock

- Image repository: `martialblog/limesurvey`
- Image tag: `6.16.10-260223-apache` (pinned, not `latest`)
- Release lock ConfigMap: `manifests/configmap-release-lock.yaml`

## Required Edits Before Sync

1. Update `manifests/secret.yaml`:
   - `DB_HOST`
   - `DB_PORT`
   - `DB_NAME`
   - `DB_USER`
   - `DB_PASSWORD`
2. Optional: adjust `manifests/external-db-svc.yaml` if you use another DB hostname.
3. Optional: customize branding in `manifests/configmap-branding.yaml`.
4. Change admin bootstrap password in `manifests/deployment.yaml` (`ADMIN_PASSWORD`).

## Argo CD Application

- File: `application.yaml`
- Source path: `apps/limesurvey/manifests`
- Sync policy: automated (`prune + selfHeal`)

Apply once in Argo namespace (if this app is not yet managed by a parent app):

```bash
kubectl apply -n argocd -f apps/limesurvey/application.yaml
```

## Ingress

- Host: `forms.esp.edu.kg`
- Protocol: HTTP only (no TLS yet)
