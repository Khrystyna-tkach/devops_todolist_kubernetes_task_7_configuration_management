Apply ConfigMap

The configMap.yml file contains the PYTHONUNBUFFERED environment variable.

Apply ConfigMap:

kubectl apply -f .infrastructure/configMap.yml

Verify ConfigMap:

kubectl get configmap todoapp-config -n mateapp
kubectl describe configmap todoapp-config -n mateapp

Expected value:

PYTHONUNBUFFERED: 1

Apply Secret

kubectl apply -f .infrastructure/secret.yml

Verify that the Secret exists:

kubectl get secret todoapp-secret -n mateapp

Check the Secret keys without displaying their values:

kubectl describe secret todoapp-secret -n mateapp

Apply Deployment

The Deployment uses ConfigMap and Secret through environment variables:

PYTHONUNBUFFERED — loaded from ConfigMap todoapp-config.

SECRET_KEY — loaded from Secret todoapp-secret.

Apply the updated Deployment:

kubectl apply -f .infrastructure/deployment.yml

Check the rollout status:

kubectl rollout status deployment/todoapp -n mateapp

Validate Changes

Check all resources:

kubectl get configmaps -n mateapp
kubectl get secrets -n mateapp
kubectl get deployments -n mateapp
kubectl get pods -n mateapp
