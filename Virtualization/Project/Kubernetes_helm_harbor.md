# 쿠버네티스 Helm차트로 Harbor구성하기
## 실습 목차
1. Add Harbor Chart Repository

2. Make values.yaml
    PVC
    Domain
    Password
    ...

3. Create Namespace

4. Install Harbor Chart

5. Edit /etc/hosts with Client/All Nodes

6. Verify Harbor Portal

7. Add library(harbor) Chart Repository with Cert(ca.crt)

8. Allow Insecure Harbor Registry with All nodes
https://docs.docker.com/registry/insecure/
    1) /etc/docker/daemon.json
    2) /etc/docker/certs.d/<domain>/ca.crt

9. Create secret for Authentication of Harbor Registry 

출처: https://github.com/goharbor/harbor-helm
