```

4 балла:
docker build -t hw3-first .
docker run -d --name hw3-1 -p 127.0.0.1:8080:8000 -e GREETING='Привет из Docker!' hw3-first
curl http://127.0.0.1:8080/
Вывод: {"greeting": "Привет из Docker!", "count": 0, "hostname": "521971319def", "storage": "sqlite"}

curl -X POST http://127.0.0.1:8080/increment
Вывод: {"greeting": "Привет из Docker!", "count": 1, "hostname": "521971319def", "storage": "sqlite"}

curl http://127.0.0.1:8080/
Вывод: {"greeting": "Привет из Docker!", "count": 1, "hostname": "521971319def", "storage": "sqlite"}


docker logs hw3-1
Вывод:
2026-11-06 10:32:14,079 listening port=8000 storage=sqlite
2026-11-06 10:32:21,407 http 172.17.0.1 "GET / HTTP/1.1" 200 -
2026-11-06 10:32:21,419 http 172.17.0.1 "POST /increment HTTP/1.1" 200 -
2026-11-06 10:32:21,427 http 172.17.0.1 "GET / HTTP/1.1" 200 -



6 баллов:
Это задание выполнила с версией compose.yaml для SQLite.
docker compose up -d --build
curl -X POST http://127.0.0.1:8080/increment
Вывод: {"greeting": "Hello, Docker!", "count": 1, "hostname": "d2d662850751", "storage": "sqlite"}

docker compose down
docker compose up -d --build
curl http://127.0.0.1:8080/
Вывод: {"greeting": "Hello, Docker!", "count": 1, "hostname": "705c47c4daf3", "storage": "sqlite"}


8 баллов:
curl -X POST http://127.0.0.1:8080/increment
Вывод: {"greeting": "Hello, Docker!", "count": 1, "hostname": "156780253c56", "storage": "redis"}

curl -X POST http://127.0.0.1:8080/increment
Вывод: {"greeting": "Hello, Docker!", "count": 2, "hostname": "156780253c56", "storage": "redis"}

docker compose down
Вывод:
 ✔ Container hw_3_ipr-app-1   Removed
 ✔ Container hw_3_ipr-redis-1 Removed
 ✔ Network hw_3_ipr_default   Removed

docker compose up -d --wait
Вывод:
 ✔ Network hw_3_ipr_default   Created
 ✔ Container hw_3_ipr-redis-1 Healthy
 ✔ Container hw_3_ipr-app-1   Healthy

curl http://127.0.0.1:8080/
Вывод: {"greeting": "Hello, Docker!", "count": 2, "hostname": "fc7d1268a4ca", "storage": "redis"}
Счетчик остался равен 2.

docker compose stop redis
Вывод: Container hw_3_ipr-redis-1 Stopped

curl -i http://127.0.0.1:8080/healthz
Вывод: HTTP/1.0 200 OK
{"status": "alive"}

curl -i http://127.0.0.1:8080/readyz
Вывод: HTTP/1.0 503 Service Unavailable
{"error": "storage_unavailable"}

curl -i -X POST http://127.0.0.1:8080/increment
Вывод: HTTP/1.0 503 Service Unavailable
{"error": "storage_unavailable"}

docker compose start redis
Вывод: Container hw_3_ipr-redis-1 Started

curl http://127.0.0.1:8080/
Вывод: {"greeting": "Hello, Docker!", "count": 2, "hostname": "fc7d1268a4ca", "storage": "redis"}

curl -X POST http://127.0.0.1:8080/increment
Вывод: {"greeting": "Hello, Docker!", "count": 3, "hostname": "fc7d1268a4ca", "storage": "redis"}
```
