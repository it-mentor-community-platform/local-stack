# Импорт дашборда Grafana

## Автоматический импорт (через provisioning)

1. Скопируй json файл с дашбордом  в папку `grafana/provisioning/dashboards/`
2. Перезапусти Grafana: `docker-compose restart grafana`
3. Дашборд появится в папке `import` в Grafana UI `http://localhost:3000`

## Ручной импорт (через UI)

1. Открой Grafana: `http://localhost:3000`
2. Боковое меню → **Dashboards** → **New** →**Import**
3. Перемести json фаил в окошко **Upload dashboard JSON file**
4. Выбери источник данных **Prometheus**
5. Нажми **Import**

default.yaml - фаил конфигурации автоматического добавления дашборда в Grafana UI