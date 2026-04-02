# 📦 OAuth2 Authorization / Resource Server kustomize

## 🧪 Testing

### Token 발급

```bash
curl -u client:secret \
  -X POST https://localhost:8080/oauth2/token \
  -H "Host: auth.ythwork.com" \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -d "grant_type=urn:ietf:params:oauth:grant-type:password&username=user&password=1234&scope=read" \
  -k -v
```


---

### Resource Server 호출

```bash
curl -H "Host: resource.ythwork.com" \
-H "Authorization: Bearer <access_token>" \
https://localhost:8080/api/read \
-k -v
```
