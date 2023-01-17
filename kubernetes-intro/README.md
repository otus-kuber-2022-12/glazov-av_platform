# выполнено ДЗ № 1

## в процессе сделано
- установил docker, minikube, kubectl, k9s, настроил автодополнение kubectl для bash
- удалил контейнеры с системными компонентами, они восстановились поскольку описаны в 
~~~
docker@minikube:~$ ls -la /etc/kubernetes/manifests/
total 28
drwxr-xr-x 1 root root 4096 Dec 26 13:29 .
drwxr-xr-x 1 root root 4096 Dec 26 13:29 ..
-rw------- 1 root root 2470 Dec 26 13:29 etcd.yaml
-rw------- 1 root root 4076 Dec 26 13:29 kube-apiserver.yaml
-rw------- 1 root root 3395 Dec 26 13:29 kube-controller-manager.yaml
-rw------- 1 root root 1441 Dec 26 13:29 kube-scheduler.yaml
~~~
подом core-dns управляет deployment, он и восстановил
- написал Docker файл который создает образ на основе nginx на 8000 порту отдающего все содержимое каталога /app в контейнере, создал образ и запушил его в docker hub
- написал и применил манифест web-pod.yaml для создания pod web содержащий один контейнер с названием web использующий образ залитый ранее на docker hub
- добавил в pod init контейнер генерирующий страницу index.html в общий с контейнером web volumeMounts, запустил pod, init создал страницу, web отдал ее по http://localhost:8000/index.html

## задание со *
- сгенерировал манифест yaml командой kubectl run frontend --image avtandilko/hipster-frontend:v0.0.1 --restart=Never --dry-run -o yaml > frontend-pod.yaml
- после применения манифеста pod запустился и встал в ошибку, чтение логов выявило отсутствие ряда переменных окружения необходимых для работы приложения
- создал исправленный манифест frontend-pod-healfy.yaml и pod запустился корректно
