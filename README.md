# Local Stack

## Основная информация
Локальное окружение представляет собой Docker Compose стек из контейнеров для каждого сервиса и базы данных.
Каждый разработчик может запустить все сервисы локально что бы при необходимости использовать их во время разработки 
своего сервиса.

Порты всех сервисов прокинуты наружу для доступа к ним извне Compose стека в целях разработки и тестирования.
При этом сами сервисы, запущенные внутри контейнеров, используют профиль local-stack, и обращаются к другим сервисам по
их именам (пример - если сервис Postgres называется database, другие сервисы будут обращаться к нему по адресу 
database:5432).

## Список сервисов

* **База данных**
  - внутреннее название/порт: `database:5432`
  - внешний порт: `5432`
  - логин: `root`
  - пароль: `password`
  - Имя БД схемы: `it_mentor_community_platform`
* **Gateway**
    - внутреннее название/порт: `gateway:8080`
    - внешний порт: `8080`
* **Auth service**
    - внутреннее название/порт: `auth-service:8080`
    - внешний порт: `8081`
* **Data importer**
    - внутреннее название/порт: `data-importer:8080`
    - внешний порт: `8082`
* **Project Service**
  - внутреннее название/порт: `project-service:8080`
  - внешний порт: `8084`
* **Prometheus**
    - внутреннее название/порт: `prometheus:9090`
    - внешний порт: `9090`
* **Grafana**
    - внутреннее название/порт: `grafana:3000`
    - внешний порт: `3000`
* **Profile Service**
    - внутреннее название/порт: `profile-service:8080`
    - внешний порт: `8083`
* **Kafka**
    - внутреннее название/порт: `kafka:9092`
    - внешний порт: `29092`
* **Kafka-UI**
    - внутреннее название/порт: `kafka-ui:8080`
    - внешний порт: `8088`

## Необходимая инфраструктура

- Docker
- Docker Compose


## Инструкция по запуску контейнеров
- Для сервиса Data Importer необходим файл credentials.json. Запроси его у тимлида(или в Secrets на GitHub) и скопируй в корень проекта.
- Убедитесь, что Docker и Docker Compose установлены.
- В корне проекта выполните:
    ```sh
    docker compose pull
    docker compose up -d
    ```
    или
    ```sh
    docker compose up -d --pull always
    ```
  Ключ `--pull always` необходим для того, чтобы перед запуском образы обновлялись до последней версии.

### Приватный репозиторий
  ```sh
     ✘ Error Head "https://ghcr.io/v2/it-mentor-community-platform/.../dev": unauthorized
    Error response from daemon: Head "https://ghcr.io/v2/it-mentor-community-platform/.../dev": unauthorized
  ```
Если вы увидите подобное сообщение, значит репозиторий GitHub Container Registry приватный, и вам нужно
ваш докер авторизовать на ghrc.io, а так же иметь права доступа к этому репозиторию. <br>
Что бы залогиниться используйте команду
  ```shell
    echo "YOUR_GITHUB_TOKEN" | docker login ghcr.io -u YOUR_GITHUB_USERNAME --password-stdin
  ```
или
  ```shell
    docker login ghcr.io -u YOUR_GITHUB_USERNAME -p YOUR_GITHUB_TOKEN
  ```
**Что бы создать GITHUB_TOKEN (PAT)**

1. Перейдите: https://github.com/settings/tokens
2. Generate new token → Classic
3. Выбери права:
   - read:packages — обязательно (для скачивания)
   - write:packages — если будешь пушить
   - delete:packages — если нужно удалять
4. Скопируй токен (он покажется только один раз)

## Секреты

Все секреты можно устанавливать как переменные окружения в терминале, где вы запускаете compose стек, или через .env файл в папке с docker-compose файлом.

### TELEGRAM_BOT_TOKEN

Инструкция по получению и использованию токена описана в README.md auth-service по  [ссылке](https://github.com/it-mentor-community-platform/auth-service?tab=readme-ov-file#%D0%B0%D0%B2%D1%82%D0%BE%D1%80%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D1%8F-%D1%87%D0%B5%D1%80%D0%B5%D0%B7-telegram).

## Ссылки на репозиторий документации
- [Окружения и профили](https://github.com/it-mentor-community-platform/meta/blob/main/system-analytics/environments-and-profiles.md)
