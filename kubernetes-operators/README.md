glazov-av@otus-domashka:~/glazov-av_platform/kubernetes-operators$ kubectl get jobs
NAME                         COMPLETIONS   DURATION   AGE
backup-mysql-instance-job    1/1           5s         11m
restore-mysql-instance-job   1/1           46s        9m23s

glazov-av@otus-domashka:~/glazov-av_platform/kubernetes-operators$ export MYSQLPOD=$(kubectl get pods -l app=mysql-instance -o jsonpath="{.items[*].metadata.name}")
glazov-av@otus-domashka:~/glazov-av_platform/kubernetes-operators$ kubectl exec -it $MYSQLPOD -- mysql -potuspassword -e "select * from test;" otus-database
mysql: [Warning] Using a password on the command line interface can be insecure.
+----+-------------+
| id | name        |
+----+-------------+
|  1 | some data-1 |
|  2 | some data-2 |
|  3 | some data-3 |
+----+-------------+
