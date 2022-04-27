# Projeto Final do Curso de Big Data Engineer da Semantix Academy

## Projeto Básico

O projeto executado foi o nível básico, que junta os dados da Campanha Nacional de Vacinação contra Covid-19 e faz uma série de armazenamentos em locais específicos e visualizações.

O documento com as especificações do projeto pode ser acessado [aqui](https://github.com/viccsouza/projeto_covidbr/blob/main/documents/projeto_final_spark.pdf).

O projeto foi executado utilizando WSL com docker, e parte da execução foi utilizando Pyspark em um Jupyter-Notebook que pode ser acessado [aqui](https://github.com/viccsouza/projeto_covidbr/blob/main/pyspark/projeto_b%C3%A1sico.ipynb).

## Preparação do Ambiente:
Para o projeto, foi montado um docker-compose fornecido pela Semantix Academy durante suas aulas, com as seguintes imagens:

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

É possível baixar os componentes do cluster [aqui](https://github.com/rodrigo-reboucas/docker-bigdata.git), o arquivo utilizado foi o _docker-compose-parcial.yml_.

## Questão 1 - Enviar os Dados para o HDFS

#### Baixar e extrair os dados no local do Docker para envio para o HDFS:
```sh
cd /input/

curl -O https://mobileapps.saude.gov.br/esus-vepi/files/unAFkcaNDeXajurGB7LChj8SgQYS2ptm/04bd3419b22b9cc5c6efac2c6528100d_HIST_PAINEL_COVIDBR_06jul2021.rar

unrar x 04bd3419b22b9cc5c6efac2c6528100d_HIST_PAINEL_COVIDBR_06jul2021.rar
```

#### Criar a pasta base e passar os arquivos para o hdfs:
Após acessar o container namenode no docker.

```
hdfs dfs -mkdir -p /user/projeto_basico/dados
hdfs dfs -put /input/*.csv /user/projeto_basico/dados
```



#### Verificar a transferência:
```
hdfs dfs -ls -h /user/projeto_basico/dados
```
_output:_

>Found 4 items  
-rw-r--r--   3 root supergroup     59.6 M 2022-04-26 23:35 /user/projeto_basico/dados/HIST_PAINEL_COVIDBR_2020_Parte1_06jul2021.csv  
-rw-r--r--   3 root supergroup     73.0 M 2022-04-26 23:35 /user/projeto_basico/dados/HIST_PAINEL_COVIDBR_2020_Parte2_06jul2021.csv  
-rw-r--r--   3 root supergroup     86.9 M 2022-04-26 23:35 /user/projeto_basico/dados/HIST_PAINEL_COVIDBR_2021_Parte1_06jul2021.csv  
-rw-r--r--   3 root supergroup      2.9 M 2022-04-26 23:35 /user/projeto_basico/dados/HIST_PAINEL_COVIDBR_2021_Parte2_06jul2021.csv


