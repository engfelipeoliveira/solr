# solr

1. Instalar Java
sudo apt-get update
sudo apt-get install openjdk-11-jdk

https://docs.datastax.com/en/jdk-install/doc/jdk-install/installOpenJdkDeb.html


2. Instalar Solr
sudo wget https://apache.mirror.colo-serv.net/lucene/solr/8.7.0/solr-8.7.0.tgz
sudo tar xzf solr-8.7.0.tgz solr-8.7.0/bin/install_solr_service.sh --strip-components=2
sudo bash ./install_solr_service.sh solr-8.7.0.tgz -f

https://tecadmin.net/install-apache-solr-on-ubuntu/
https://tecadmin.net/install-apache-solr-on-ubuntu-20-04/


3. Aumentar memoria do Solr (CONFIRMAR)
sudo vi /etc/default/solr.in.sh
SOLR_HEAP="12g"


4. Adicionar jar jdbc
/opt/solr/server/lib/ext


5. start/stop linux
sudo service solr stop
sudo service solr start
sudo service solr status

ps aux | grep solr
sudo rm /var/solr/solr-8983.pid


6. Criar nova colecao
sudo su - solr -c "/opt/solr/bin/solr create -c produtos -n data_driven_schema_configs"


7. Adicionar arquivos de configuracao
/var/solr/data/produtos
db-config.xml
schema.xml
solrconfig.xml


8. Alterar arquivo de configuracao /var/solr/data/produtos/core.properties
name=produtos
config=solrconfig.xml
schema=schema.xml
dataDir=data


9. Atualizar arquivos de configuracao
Apos atualizar os arquivos de configuracao, apagar arquivos do diretorio /var/solr/data/products/conf


10. CURL data import
curl -d "command=full-import&verbose=false&clean=false&commit=true&core=usager&name=dataimport" -H "Content-Type: application/x-www-form-urlencoded" -X POST http://localhost:8983/solr/usager/dataimport?indent=on
curl -d "command=delta-import&verbose=false&clean=false&commit=true&core=usager&name=dataimport" -H "Content-Type: application/x-www-form-urlencoded" -X POST http://localhost:8983/solr/usager/dataimport?indent=on


11. Apagar registros
http://localhost:8983/solr/#/usager/documents
/update
XML
<add><delete><query>*:*</query></delete></add>

12. Crontab
https://crontab.guru/#*/15_04-23_*_*_*
https://crontab.guru/#0_1_*_*_*
https://www.google.com/amp/s/www.digitalocean.com/community/tutorials/how-to-use-cron-to-automate-tasks-ubuntu-1804-fr.amp