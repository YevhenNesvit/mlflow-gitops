# MLflow GitOps Repository

Цей репозиторій містить конфігурації ArgoCD Applications для автоматичного деплою MLflow у Kubernetes кластер.

## 📁 Структура

```
mlflow-gitops/
├── application.yaml    # ArgoCD Application для MLflow
└── README.md          # Цей файл
```

## 🚀 Використання

### 1. Застосування Application

```bash
kubectl apply -f application.yaml
```

### 2. Перевірка статусу

```bash
kubectl get application mlflow -n infra-tools
```

## ⚙️ Конфігурація MLflow

Application налаштовано з наступними параметрами:

- **Chart**: `mlflow` від community-charts
- **Version**: `0.7.19`
- **Namespace**: `mlflow` (створюється автоматично)
- **Persistence**: 10GB PVC
- **Resources**: 250m CPU / 512Mi Memory (requests)

## 🔄 Auto-Sync

Application налаштовано на автоматичну синхронізацію:
- `prune: true` - видаляє застарілі ресурси
- `selfHeal: true` - автоматично відновлює ресурси
- `CreateNamespace=true` - автоматично створює namespace

## 📝 Зміни конфігурації

Щоб змінити конфігурацію MLflow:

1. Відредагуйте секцію `helm.values` у `application.yaml`
2. Зробіть commit та push
3. ArgoCD автоматично застосує зміни протягом 3 хвилин

## 🔍 Моніторинг

Переглядайте статус деплою:
- ArgoCD UI: http://localhost:8080
- MLflow UI: http://localhost:5000 (після port-forward)

```bash
# Port-forward до MLflow
kubectl port-forward svc/mlflow -n mlflow 5000:5000
```