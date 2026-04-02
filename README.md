# 📦 OAuth2 Authorization / Resource Server kustomize

## 🧪 Testing

### ingress controller 서비스 포트포워딩
  - 리눅스의 경우 /etc/hosts에 도메인을 추가하면 된다.
    - auth.ythwork.com
    - resource.ythwork.com
  - macos이고 docker-desktop 싱글 노드 클러스터일 때 /etc/hosts를 변경해도 안되는 경우가 있는데 이때는 아래와 같이 진행하고 TLS를 적용하기 위해 ingress controller 서비스를 포트포워딩한다.

```bash
kubectl port-forward -n ingress-nginx svc/ingress-nginx-controller 8080:443
```
---

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
