# Modulo 03

Generar certificado autofirmados

```bash
openssl req -x509 -newkey rsa:2048 -nodes \
-keyout ~/keycloak-certs/tls.key \
-out ~/keycloak-certs/tls.crt \
-days 3650 \
-subj "/CN=keycloak/O=pruebas" \
-addext "subjectAltName=IP:192.168.56.201,DNS:keycloak"
```
Generar el siguiente secreto

```bash
kubectl create secret tls keycloak-tls-secret \
--cert=$HOME/keycloak-certs/tls.crt \
--key=$HOME/keycloak-certs/tls.key \
-n keycloak
```

Copiar el certificado al siguiente directorio.

```bash
cp ~/keycloak-certs/tls.crt /etc/kubernetes/pki/keycloak-ca.crt
```

Ejecutar el siguiente comando con el archivo yaml

```bash
kubectl apply -f 01-keycloak-tls.yaml
```

En el archivo `/etc/kubernetes/manifests/kube-apiserver.yaml`

```yaml
    - --oidc-issuer-url=https://192.168.56.201:30443/realms/kubernetes-demo
    - --oidc-client-id=kubernetes
    - --oidc-username-claim=preferred_username
    - --oidc-groups-claim=groups
    - --oidc-groups-prefix=keycloak-
    - --oidc-ca-file=/etc/kubernetes/pki/keycloak-ca.crt
```
