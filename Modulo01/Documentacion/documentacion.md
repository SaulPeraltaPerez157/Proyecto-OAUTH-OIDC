# Módulo 1

Crear el namespace.

```bash
kubectl create namespace keycloak
```

Crear el secreto.

```bash
kubectl create secret generic keycloak-admin \
--from-literal=KEYCLOAK_ADMIN=admin \
--from-literal=KEYCLOAK_ADMIN_PASSWORD=Admin1234! \
-n keycloak
```

Ejecutar el archivo yaml.

```bash
kubectl apply -f 01-keycloak.yaml
```

Acceder desde la ip del nodo k8s-worker01

```
http://<ip_nodo>:30090
```
