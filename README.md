# Быстрый запуск
```bash
# Собрать и запустить
docker-compose up -d

# Доступ
Frontend: http://localhost
Backend: http://localhost:8081
```

# Особенности
* Мульти-контейнерная архитектура
* Healthcheck-проверки
* Ограничения ресурсов (CPU/RAM)
* Запуск без root-прав
* Готовность к Docker Swarm

# Образы
* Backend: Go на Alpine (~20MB)
* Frontend: Vue.js + nginx (~50MB)

# Деплой в прод
```bash
# Развернуть в Swarm
docker stack deploy -c docker-compose.yml momo-store
```

