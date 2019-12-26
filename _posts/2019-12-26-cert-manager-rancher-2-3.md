---
layout: post
title: Install Cert-Manager on Racnher 2.3
subtitle: last compatible version v0.10
---

On cluster console :

Namespace create :
```
kubectl create namespace cert-manager
```

Cert-manager v0.10 install
```
kubectl apply --validate=false -f https://github.com/jetstack/cert-manager/releases/download/v0.10.0/cert-manager.yaml
```

Test if Cert-Manager ready 
```
kubectl get pods --namespace cert-manager
```

Result :
```
NAME                                       READY   STATUS    RESTARTS   AGE
cert-manager-57c65cb5f5-jfp4w              1/1     Running   0          28m
cert-manager-cainjector-6f868ccdf6-fhmdm   1/1     Running   0          28m
cert-manager-webhook-5896b5fb5c-grfnw      1/1     Running   0          28m
```

Define issuer
```
cat <<EOF > issuer.yaml
apiVersion: certmanager.k8s.io/v1alpha1
kind: Issuer
metadata:
  name: letsencrypt-prod
  namespace: default
spec:
  acme:
    # The ACME server URL
    server: https://acme-v02.api.letsencrypt.org/directory
    # Email address used for ACME registration
    email: test@example.com
    # Name of a secret used to store the ACME account private key
    privateKeySecretRef:
      name: letsencrypt-prod
    # Enable the HTTP-01 challenge provider
    solvers:
    # An empty 'selector' means that this solver matches all domains
    - selector: {}
      http01:
        ingress:
          class: nginx
EOF
```

Apply issuer
```
kubectl apply -f issuer.yaml
```

Define Cert 
```
cat <<EOF > my-cert.yaml
apiVersion: certmanager.k8s.io/v1alpha1
kind: Certificate
metadata:
  name: my-cert-crt
  namespace: default
spec:
  secretName: my-cert-tls
  issuerRef:
    name: letsencrypt-prod
  commonName: my.cert.io
EOF

```
Apply Cert
```
kubectl apply -f my-cert.yaml
```

Your Cert are now avaible in your load balancing