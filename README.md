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
- https://github.com/suxarikisme/endgame/blob/master/.github/workflows/ci-queue-master.yml
- https://github.com/suxarikisme/endgame/blob/master/.github/workflows/ci-queue-carts.yml
- https://github.com/suxarikisme/endgame/blob/master/.github/workflows/ci-queue-catalogue.yml
- https://github.com/suxarikisme/endgame/blob/master/.github/workflows/ci-queue-front-end.yml
- https://github.com/suxarikisme/endgame/blob/master/.github/workflows/ci-queue-orders.yml
- https://github.com/suxarikisme/endgame/blob/master/.github/workflows/ci-queue-payment.yml
- https://github.com/suxarikisme/endgame/blob/master/.github/workflows/ci-queue-shipping.yml

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

Пайплайны деплоя:
- Создание кластера в yandex cloud, установка первичных компонентов
Необходимо создать в github секреты YC_KEY и YC_FOLDER_ID, ключ от service account и идентификатор каталога соответственно
https://github.com/suxarikisme/endgame/blob/master/.github/workflows/ci-yandex-initial-sh.yml
- Создание всех приложений в ArgoCD используя argo cli
https://github.com/suxarikisme/endgame/blob/master/.github/workflows/ci-argo-apps.yml

## Описание компонент

|  App | Задача | Тип установки |
| ------ | ------ | ------ |
| Sock Shop | Демо приложение | GitHub Actions через argo cli (yaml) |
| VictoriaMetrics Cluster | Хранение метрик приложений | GitHub Actions через argo cli (helm) |
| VictoriaMetrics Agent | Сбор метрик приложений | GitHub Actions через argo cli (helm) |
| Loki/Grafana | Сбор и отображение логов | GitHub Actions через argo cli (helm) |
| ArgoCD | GitOps | GitHub Actions через argo cli (helm) |
| Jaeger | Трейсинг | GitHub Actions через argo cli (yaml) |

## Установка

- Регистрируемся в yandex cloud
- Клонируем репозиторий
- Создаем в yandex cloud service account
- Запускаем сборки приложений sock shop из пункта CD
- Заполняем secrets в github
- Запускаем ci-yandex-initial-sh.yml
- Запускаем ci-argo-apps.yml
