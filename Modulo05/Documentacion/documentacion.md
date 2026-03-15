# Modulo 5

Instalar tar

```bash
dnf install -y tar
```

Ejecutar para obtener krew

```bash
(
  set -x; cd "/tmp/tmp.vTqj8bg3sT" &&
  OS="linux" &&
  ARCH="amd64" &&
  curl -fsSLO "https://github.com/kubernetes-sigs/krew/releases/latest/download/krew-_.tar.gz" &&
  tar zxvf "krew-_.tar.gz" &&
  KREW=./krew-"_" &&
  "" install krew
)
```

Instalar oidc-login

```bash
kubectl krew install oidc-login
```

Tener a la mano el Client Secret.

Configuración de las credenciales para los usuarios.

```bash
kubectl config set-credentials <usuario>   --exec-api-version=client.authentication.k8s.io/v1beta1   --exec-command=kubectl   --exec-arg=oidc-login   --exec-arg=get-token   --exec-arg=--oidc-issuer-url=https://<ip_nodo>:30443/realms/kubernetes-demo   --exec-arg=--oidc-client-id=kubernetes   --exec-arg=--oidc-client-secret=<client_secret>   --exec-arg=--oidc-extra-scope=openid   --exec-arg=--grant-type=password   --exec-arg=--username=dev-<username>   --exec-arg=--password=<password>   --exec-arg=--certificate-authority=/etc/pki/ca-trust/source/anchors/tls.crt

kubectl config set-context dev-context   --cluster=kubernetes   --user=<username>   --namespace=<namespace_name>
```

