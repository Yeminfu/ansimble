## 1. Установка Docker

```
  ## 1.1 Обновите систему
  sudo apt update && sudo apt upgrade -y

  ## 1.2 Установите зависимости
  sudo apt install -y ca-certificates curl gnupg lsb-release

  ## 1.3 Добавьте GPG-ключ Docker
  sudo install -m 0755 -d /etc/apt/keyrings
  curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \
    sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
  sudo chmod a+r /etc/apt/keyrings/docker.gpg

  ## 1.4 Добавьте репозиторий
  echo \
    "deb [arch=$(dpkg --print-architecture) \
    signed-by=/etc/apt/keyrings/docker.gpg] \
    https://download.docker.com/linux/ubuntu \
    $(lsb_release -cs) stable" | \
    sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

  ## 1.5 Установите Docker
  sudo apt update
  sudo apt install -y docker-ce docker-ce-cli containerd.io docker-compose-plugin

  ## 1.6 Запустите Docker
  sudo systemctl start docker
  sudo systemctl enable docker
```

## 2. Настройка прав
## 2.1 Добавьте пользователя в группу docker
sudo usermod -aG docker $USER

## 2.2 Примените изменения (важно!)
newgrp docker

## 2.3 Проверьте установку
docker --version
docker compose version
docker run hello-world

## 3. Запуск PostgreSQL
## 3.1 Запустите контейнер
docker run --name postgres-db \
  -e POSTGRES_PASSWORD=secret123 \
  -e POSTGRES_DB=mydb \
  -e POSTGRES_USER=myuser \
  -v postgres_/var/lib/postgresql/data \
  -p 5432:5432 \
  -d postgres:15-alpine

## 3.2 Проверьте статус
docker ps | grep postgres

## 3.3 Посмотрите логи (если есть проблемы)
docker logs postgres-db

## 4. Подключение к базе
docker exec -it postgres-db psql -U myuser -d mydb

SELECT version(); -- версия PostgreSQL
