Алгоритм выполнения задания в Apache Hadoop

Развернуть образ конфигурации  ds_mgpu_Hadoop3+spark_3_4 https://disk.yandex.ru/d/zEKP6GY6Nosaxg  

Все дальнейшие действия выполняются пользователем hadoop.
$ sudo su - hadoop

Шаг 1. Запуск Hadoop.
$ start-dfs.sh
$ start-yarn.sh

Шаг 2. Проверка работы Hadoop.
$ jps

В стандартной конфигурации Hadoop HDFS предоставляет веб-интерфейсы:
-	HDFS NameNode: http://localhost:9870 
-	YARN ResourceManager: http://localhost:8088

установить разрешение на запись для всех пользователей
$ hdfs dfs -chmod 775 /user2/hadoop/economic_data

разрешить запись только пользователю devops
$ hdfs dfs -setfacl -m user:devops:rwx /user3/hadoop/economic_data

Для того чтобы загрузить все файлы из локальной папки `~/Downloads/lab_1_2/data` в HDFS в папку `sparkdir`, выполните следующие шаги:

### Шаг 1. Создание папки в HDFS

Для начала создадим каталог `sparkdir` в HDFS:

```bash
hdfs dfs -mkdir -p /user5/sparkdir
```

Замените `devops` на имя пользователя, если это необходимо.

### Шаг 2. Загрузка файлов в HDFS

Теперь, когда папка `sparkdir` создана, нужно загрузить все файлы из локальной директории в HDFS.

Для этого используйте команду `hdfs dfs -put`:

```bash
hdfs dfs -put /home/hadoop/Downloads/lab_01_2/lab_1_2/data/* /user5/sparkdir/
```

Эта команда загрузит все файлы из папки `/home/hadoop/Downloads/lab_01_2/lab_1_2/data/` в папку `sparkdir` на HDFS.

### Шаг 3. Проверка загрузки

Чтобы убедиться, что файлы были успешно загружены, выполните команду:

```bash
hdfs dfs -ls /user5/sparkdir/
```

Эта команда выведет список всех файлов в каталоге `sparkdir` на HDFS.

Теперь все файлы из `~/Downloads/lab_1_2/data` должны быть успешно загружены в `sparkdir` на HDFS.




Завершение работы с Hadoop

$ stop-yarn.sh
$ stop-dfs.sh

Для полной остановки всех Hadoop-демонов:
$ stop-all.sh

Проверка остановки всех процессов:
$ jps



