# Kubernetes-Deployments
Kubernetes-Deployments with 3 applications with path based routing.

This deployment provisions three web applications in Kubernetes using separate Services and Deployments and exposes them via path-based routing through an Ingress resource managed by the NGINX Ingress Controller.

Namespace: web-apps
Deployments:

nginx-deploy: NGINX (image can come from your private registry)
httpd-deploy: Apache HTTPD (image from Docker Hub)
echo-deploy: lightweight HTTP echo server (image from Docker Hub or private registry)


Services: ClusterIP services exposing port 80 for each app
Ingress: routes /<path> to respective backend:

/nginx → nginx-svc
/apache → httpd-svc
/app → echo-svc


Images: Mix of Docker Hub and your private container registry (ACR or other)
Auth: Uses imagePullSecrets for both registries (e.g., dockerhub-cred and acr-cred)
Rewrite: Uses nginx.ingress.kubernetes.io/rewrite-target: / to strip the prefix and serve content from /
