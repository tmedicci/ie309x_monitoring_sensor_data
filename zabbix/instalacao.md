# Passos para Instalação do Zabbix 4.2 no Ubunto 16.04

## Etapa 1: Atualizar o sistema
sudo apt-get update

## Etapa 2: Instalar o LAMP Server
sudo apt-get install lamp-server^

## Etapa 3: Instalar e configurar o Zabbix server
sudo wget https://repo.zabbix.com/zabbix/4.2/ubuntu/pool/main/z/zabbix-release/zabbix-release_4.2-1+xenial_all.deb
sudo dpkg -i zabbix-release_4.2-1+xenial_all.deb
sudo apt update

## Etapa 4: Instalar o Zabbix Server, Frontend e Agent
sudo apt -y install zabbix-server-mysql zabbix-frontend-php zabbix-agent

## Etapa 5: Criação da base de dados
sudo mysql -u root -p

mysql> create database zabbix character set utf8 collate utf8_bin;

mysql> grant all privileges on zabbix.* to zabbix@localhost identified by 'crie_uma_senha';

mysql> quit;

### Importar esquema e dados iniciais. Será necessário usar a senha criada anteriormente.
zcat /usr/share/doc/zabbix-server-mysql*/create.sql.gz | mysql -uzabbix -p zabbix

## Etapa 6: Configurar a base de dados para o Zabbix server
sudo nano /etc/zabbix/zabbix_server.conf

### Alterar o seguinte item, lembrando que não deve haver \# no início pois representa comentário.  
DBPassword=adicione_a_senha

## Etapa 7: Reiniciar o serviço

service apache2 restart
service zabbix-server restart

## Etapa 8: Configurar PHP para Zabbix frontend
sudo nano /etc/zabbix/apache.conf

### Descomentar e adicionar o timezone nos dois campos presentes no arquivo
php_value date.timezone America/Sao_paulo

## Etapa 9: Iniciar o Zabbix server and agent processes
systemctl restart zabbix-server zabbix-agent apache2
sudo systemctl enable zabbix-server zabbix-agent apache2

## Etapa10: Configurar o Zabbix frontend
### Anotar o ip do servidor
ifconfig
### Abrir o navegador e digitar
http://ip_anotado/zabbix
### seguir o tutorial
https://www.zabbix.com/documentation/4.2/manual/installation/install#installing_frontend

Dando tudo certo, só será necessário preencher a senha.
### Acesso
login: Admin

senha: zabbix

## Fontes
https://www.zabbix.com/download?zabbix=4.2&os_distribution=ubuntu&os_version=16.04_xenial&db=mysql
https://www.youtube.com/watch?v=2S8_YHRDWJA&list=PLcScBkZtsEB1iOB7YMPbalz1G3uVBYAMy&index=1
