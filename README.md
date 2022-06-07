# Final Project of the Big Data Engineer Course at Semantix Academy

## Basic Project

The project executed was the basic level, which gathers data from the National Vaccination Campaign against Covid-19 and makes a series of storages in specific locations and visualizations.

The document with the project specifications can be accessed [here](https://github.com/viccsouza/projeto_covidbr/blob/main/documents/projeto_final_spark.pdf).

The project was executed using WSL with docker, and part of the execution was using Pyspark in a Jupyter-Notebook that can be accessed [here](https://github.com/viccsouza/projeto_covidbr/blob/main/pyspark/projeto_b%C3%A1sico.ipynb).

## Environment Preparation:
For the project, a docker-compose provided by Semantix Academy during its classes was assembled, with the following images:

> namenode: fjardim/namenode_sqoop  
datanode: fjardim/datanode  
hive-server: fjardim/hive  
hive-metastore: fjardim/hive  
hive-metastore-postgresql: fjardim/hive-metastore  
database: fjardim/mysql  
zookeeper: fjardim/zookeeper  
kafka: fjardim/kafka  
hbase-master: fjardim/hbase-master  
mongo: fjardim/mongo  
mongo-express: fjardim/mongo-express  
kafkamanager: fjardim/kafkamanager  
jupyter-spark: fjardim/jupyter-spark

Is it possible to download docker components [here](https://github.com/rodrigo-reboucas/docker-bigdata.git), the compose file used was the _docker-compose-parcial.yml_.

## Question 1 - Send Data to HDFS

#### Download and extract the data in Docker for uploading to HDFS:
```sh
cd /input/

curl -O https://mobileapps.saude.gov.br/esus-vepi/files/unAFkcaNDeXajurGB7LChj8SgQYS2ptm/04bd3419b22b9cc5c6efac2c6528100d_HIST_PAINEL_COVIDBR_06jul2021.rar

unrar x 04bd3419b22b9cc5c6efac2c6528100d_HIST_PAINEL_COVIDBR_06jul2021.rar
```

#### Create the base folder and send the files to hdfs:
After accessing the namenode container in docker.

```
hdfs dfs -mkdir -p /user/projeto_basico/dados
hdfs dfs -put /input/*.csv /user/projeto_basico/dados
```



#### Check transfer:
```
hdfs dfs -ls -h /user/projeto_basico/dados
```
_output:_

>Found 4 items  
-rw-r--r--   3 root supergroup     59.6 M 2022-04-26 23:35 /user/projeto_basico/dados/HIST_PAINEL_COVIDBR_2020_Parte1_06jul2021.csv  
-rw-r--r--   3 root supergroup     73.0 M 2022-04-26 23:35 /user/projeto_basico/dados/HIST_PAINEL_COVIDBR_2020_Parte2_06jul2021.csv  
-rw-r--r--   3 root supergroup     86.9 M 2022-04-26 23:35 /user/projeto_basico/dados/HIST_PAINEL_COVIDBR_2021_Parte1_06jul2021.csv  
-rw-r--r--   3 root supergroup      2.9 M 2022-04-26 23:35 /user/projeto_basico/dados/HIST_PAINEL_COVIDBR_2021_Parte2_06jul2021.csv


### The following questions can be accessed [here](https://github.com/viccsouza/projeto_covidbr/blob/main/pyspark/projeto_b%C3%A1sico.ipynb).
