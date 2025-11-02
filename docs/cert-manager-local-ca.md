
## Reading Material

- https://cert-manager.io/docs/configuration/selfsigned/
- https://cert-manager.io/docs/configuration/ca/

## A note about CA issuer certs issued by a self signed issuer

- https://cert-manager.io/docs/configuration/selfsigned/#certificate-validity
  - basically, always make sure to set a `Subject` for `SelfSigned` certs. Apprently, the `commonName` parameter is a shorthand for the more verbose `subject`. See

```bash
k explain certificate.spec.commonName
```

and
```bash
k explain certificate.spec.subject
```
