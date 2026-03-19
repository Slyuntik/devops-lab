# DevOps Lab: Flask app → Docker → Kubernetes

Учебный проект, демонстрирующий полный путь приложения: от кода до деплоя в Kubernetes.

## Краткое описание проекта

- `app/` - Flask приложение (Python)
- `nginx/` - конфигурация Nginx reverse proxy
- `k8s/` - манифесты Kubernetes (Deployment + Service)
- `docker-compose.yml` - локальный запуск с Nginx

## Быстрый старт

### 1. Docker
```bash
cd app
docker build -t devops-lab:v1 .
docker run -d --name lab-app -p 5000:5000 devops-lab:v1
curl http://localhost:5000
```

### 2. Docker Compose + Nginx
```bash
docker compose up -d --build
curl http://localhost
```

### 3. Kubernetes (Minikube)
```bash
minikube start
eval $(minikube docker-env)
docker build -t devops-lab:v1 ./app
kubectl apply -f k8s/deployment.yaml
kubectl apply -f k8s/service.yaml
minikube service devops-lab-service --url
```
