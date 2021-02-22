0) Create namespace "myapp"
kubectl create namespace myapp

1) Deploy db
cd postgres
kubectl apply -f postgres-deployment.yaml
**** MIGRATIONS ***

2) Deploy api-gateway
cd ..
cd auth-app
helm install auth-app ./auth-app-chart

3) Deploy app
cd ..
cd app
helm install app ./app-chart

4) Apply auth-ingress
kubectl apply -f auth_app_ingress.yaml

5) Apply app-ingress
kubectl apply -f app_ingress.yaml


If you want to execute collection again, drop users table records:
> kubectl exec --stdin --tty pod/postgres-statefulset-0 -- psql -U myuser myapp
> DELETE FROM users WHERE name IS NOT NULL;