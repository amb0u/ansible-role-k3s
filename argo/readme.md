# argo
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml


# UI
kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'

or

kubectl port-forward svc/argocd-server -n argocd 8080:443

# admin ui password
kubectl get secret argocd-initial-admin-secret -n argocd -o jsonpath="{.data.password}" | base64 -d



kubectl get secret argocd-secret -n argocd -o yaml > current-secret.yml

data:
  admin.readonly: cmVhZG9ubHk=
  # ... other existing data
kubectl apply -f current-secret.yml
