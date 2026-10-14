# cms-platform-gitops
Tool for gitops deployment to Kubernetes Based platforms
To start Argo:
microk8s kubectl port-forward -n argocd service/argocd-server 8080:443

Then go to https://localhost:8080
Run this in another terminal while argocd.sh is port-forwarding:

microk8s kubectl -n argocd get secret argocd-initial-admin-secret \  -o jsonpath="{.data.password}" | base64 -decho

Log in at https://localhost:8080 with username admin and that password. After logging in, change the initial password.

