# Prometheus

* [Source Prometheus](https://github.com/prometheus/prometheus)
* [All Repositories Prometheus](https://github.com/orgs/prometheus/repositories)

# Федеративная сеть Prometheus (Federation)

1. Запустите стек: `docker compose up -d`
2. Откройте в браузере Prometheus-Master: `http://localhost:9092`
3. В меню `Status -> Targets`, должны увидеть, что эндпоинт `prom-worker:9090/federate` находится в статусе UP
4. Вкладка `Graph`: введите имя любой метрики воркера (например, prometheus_http_requests_total). 
   Вы увидите, что к ней добавился лейбл `datacenter="dc-east-1`, но сохранились старые лейблы воркера.

Федерация через /federate отлично подходит для небольших сетей или иерархического сбора (например, стянуть 
метрики из изолированного датацентра).Однако, если вы строите глобальную отказоустойчивую систему на сотни 
контейнеров, стандарт индустрии сейчас — использовать механизм Remote Write (когда воркеры сами активно 
пушат данные в центральное хранилище вроде Grafana Mimir или Thanos).
