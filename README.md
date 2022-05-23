# CI/CD для проекта Sock Shop
## Подход GitOps-lite

Используемые технологии:
|  App | Link |
| ------ | ------ |
| YandexCloud | https://cloud.yandex.ru |
| Kubernetes | https://kubernetes.io/ |
| Kustomize | https://kustomize.io/ |
| ArgoCD | https://argo-cd.readthedocs.io/en/stable/ |
| Grafana Loki | https://grafana.com/oss/loki/ |
| Jaeger | https://www.jaegertracing.io/ |
| VictoriaMetrics | https://victoriametrics.com/ |
| Helm | https://helm.sh/ |
| GitHub + Actions | https://github.com/ |
| Sock Shop | https://github.com/microservices-demo/microservices-demo |

## Доступ
|  App | Link | auth |
| ------ | ------ | ------ |
| Sock Shop | https://51.250.86.77.nip.io | Создается |
| ArgoCD | https://argo.51.250.86.77.nip.io | admin:cluster10& |
| Grafana | https://grafana.51.250.86.77.nip.io | admin:cluster10& |
| Jaeger | https://jaeger.51.250.86.77.nip.io | - |


## CI

Сборка компонентов микросервисов выполнена на базе GitHub Actions и все пайплайны сборки находятся в репозитории.
Для хранения артефактов используется временное хранилище на базе https://ttl.sh

## CD

- Регистрируемся на yandex cloud
- Создаем service account (https://cloud.yandex.ru/docs/iam/quickstart-sa)
- Создаем yaml описание пайплайна для github actions
- Создаем кластер и группу машин в кластере
- Деплоим ingress-nginx и certificate manager
- Деплоим argocd
- Создаем через argocd cli приложения в argocd
- Смотрим и радуемся

## Описание TODO

Метрики: VictoriaMetrics Cluster Mode
Логи: Loki
GitOps: ArgoCD
Tracing: Jaeger