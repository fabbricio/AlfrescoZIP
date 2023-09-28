# Script para instalação do Alfresco versão 7.4 
Esse script irá te auxiliar na instalação do Alfresco em modo standalone utilizando os arquivos zip

## Motivação
Agilizar a instalação e configuração do Alfresco 7.4
A documentação oficial é bem rica em informações, porém eu sempre quis deixar algo mais específico e rápido para agilizar a instalação.

## Sistema operacional utilizado
Ubuntu Server 22.04 

### Pré-requisitos

```apt-get install openjdk-17-jdk openjdk-17-jre zip unzip postgresql-14```

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


