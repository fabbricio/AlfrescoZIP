# Script para instalação do Alfresco versão 7.4 
Esse script irá te auxiliar na instalação do Alfresco em modo standalone utilizando os arquivos zip

## Motivação
Agilizar a instalação e configuração do Alfresco 7.4. <br>
A documentação oficial é bem rica em informações, porém eu sempre quis deixar algo mais específico e rápido para agilizar a instalação.

## Aviso importante
Esse script tem o intuito de ajudar a quem necessita ter agilidade no processo de instalação da ferramenta na versão **community**.<br>
Não nos responsabilizamos por uso indevido desse script.<br>
Para suporte e garantias do produto utilize a versão [Enterprise edition](https://www.alfresco.com/try-alfresco)

### Endereços utilizados

Site oficial [Instalação com ZIP](https://docs.alfresco.com/content-services/latest/install/zip/)<br>
Projeto base para criar esse script. [mcgitty/install-alfresco-6x.sh](https://github.com/mcgitty/install-alfresco-6x.sh)<br>
Experimente o Alfresco [www.alfresco.com/try-alfresco](https://www.alfresco.com/try-alfresco)<br>
Alfresco [Content services](https://artifacts.alfresco.com/nexus/content/repositories/public/org/alfresco/alfresco-content-services-community-distribution/7.4.1/alfresco-content-services-community-distribution-7.4.1.zip)<br>
Alfresco [Search services](https://artifacts.alfresco.com/nexus/content/repositories/public/org/alfresco/alfresco-search-services/2.0.8/alfresco-search-services-2.0.8.zip)<br>
Alfresco [Share distribution](https://artifacts.alfresco.com/nexus/content/repositories/public/org/alfresco/alfresco-content-services-share-distribution/7.4.1/alfresco-content-services-share-distribution-7.4.1.zip)<br>
Apache [Tomcat](https://archive.apache.org/dist/tomcat/tomcat-9/v9.0.73/bin/apache-tomcat-9.0.73.zip)
PostgreSQL [JDBC](https://jdbc.postgresql.org/download/postgresql-42.5.4.jar)

### Versões utilizadas
- Alfresco versão 7.4
- Alfresco Content services 7.4.1
- Alfresco Search services 2.0.8
- Alfresco Content services share 7.4.1
- Apache Tomcat 9.0.73
- PostgreSQL 14
- Postgres JDBC **postgresql-42.5.4.jar**

### Sistema operacional utilizado
Ubuntu Server 22.04 

### Pré-requisitos

```apt-get install openjdk-17-jdk openjdk-17-jre zip unzip postgresql-14```

### Preparação do Banco de dados
Precisamos preparar o banco de dados para que o Alfresco possa criar os objetos em sua primeira carga.

```
# sudo su
# su postgres
# psql 

postgres=# create database alfresco encoding 'utf8';
postgres=# create role alfresco LOGIN password 'alfresco';
postgres=# grant all on database alfresco to alfresco;

```

# Nota
- A mensagem **Seus detalhes de autenticação não foram reconhecidos ou o Alfresco Content Services não está disponível no momento.**
É uma mensagem bem genérica, mas se todos os passos forem seguidos à risca aqui e mesmo assim a mensagem aparecer é possível que seja erro de senha.
O usuário padrão do Alfresco é **admin** e senha **admin**
- Alé do erro de senha essa mensagem pode indicar os seguintes motivos:
    - Configuração do banco de dados errada;
    - Banco de dados não foi criado;
    - O Alfresco pode não estar conseguindo se conectar com o banco de dados;
    - Verifique se o serviço do Solr subiu;

### Criar diretório de instalação
```mkdir /opt/alfresco7.4```

### Fazer o download dos arquivos para instalação
```
cd /opt/alfresco7.4
wget https://artifacts.alfresco.com/nexus/content/repositories/public/org/alfresco/alfresco-content-services-community-distribution/7.4.1/alfresco-content-services-community-distribution-7.4.1.zip
wget https://artifacts.alfresco.com/nexus/content/repositories/public/org/alfresco/alfresco-search-services/2.0.8/alfresco-search-services-2.0.8.zip
wget https://artifacts.alfresco.com/nexus/content/repositories/public/org/alfresco/alfresco-content-services-share-distribution/7.4.1/alfresco-content-services-share-distribution-7.4.1.zip	
wget https://archive.apache.org/dist/tomcat/tomcat-9/v9.0.73/bin/apache-tomcat-9.0.73.zip
```

### Executar o script "alfresco_install.sh" passando o diretório de instalação
```. /opt/AlfrescoZip/alfresco_install.sh /opt/alfresco7.4```


### Iniciar e parar o Alfresco
```
cd /opt/alfresco7.4
./alfresco.sh start
./alfresco.sh jpda start # Iniciar com debug
./alfresco.sh stop
```

### Iniciar e parar o serviço do Solr 6
```
search-services/solr/bin/solr start
search-services/solr/bin/solr stop
```