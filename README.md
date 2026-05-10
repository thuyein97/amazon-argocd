## gitops (ArgoCD app-of-apps)

This folder represents the **GitOps repo**.

### Repo
- `https://github.com/thuyein97/gitops.git`

### Key idea
- `clusters/cluster-config.yaml` is the **handshake bridge file** written by Terraform.
- `root/` is the **app-of-apps** entrypoint ArgoCD syncs first.
- `base/` contains cluster-wide prerequisites.
- `apps/` contains your business applications.

### Dependency mapping (base → apps)
- `root/base-app.yaml` syncs `base/` (Ingress, monitoring, CSI drivers, etc).
- `root/apps-app.yaml` syncs `apps/` and is annotated with `sync-wave: "1"` so it runs after base.

