
## Домашнее задание к занятию Troubleshooting

Кластер K8s

![alt text](../img/minikube.png)

Установить приложение по команде:

![alt text](../img/error1.png)

Ошибка: не созданы namespace `web` и `data`

Что сделано:

Скачан файл и добавлено создание namespace

![alt text](../img/wget.png)

![alt text](../img/namespace.png)

Манифест применён 

![alt text](../img/manifest.png)

Ошибка: `[DEPRECATION NOTICE] Docker Image Format v1 and Docker Image manifest version 2, schema 1 support is disabled by default`

![alt text](../img/error2.png)

Меняем имадж на более актуальный 

```yaml
image: alpine/curl:8.14.1
```

Всё исправлено, результат работы:

![alt text](../img/lens_success.png)


