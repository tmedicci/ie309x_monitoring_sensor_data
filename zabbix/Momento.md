# Medir o minuto e segundo

## Fazer Script para informar o tempo HHMMSS
nano contador.sh

### escrever o seguinte codigo
\#! /bin/bash
echo "Quanto tempo?"
segundos=`date +%s`
tempo=`date -d @$segundos +%H:%M:%S`
echo " MMSS: $tempo "
echo "fim"

### estabelecer permissões

chmod 777 contador.sh

## Editar Configuração do Zabbix Agent
sudo nano /etc/zabbix/zabbix_agentd.conf

### Editar a opção Parametro de usuário (Option: UserParameter)

UserParameter=ScriptMinSeg,./contador.sh | grep ':' | awk '{print $2}' | sed 's/:/./g

## Reiniciar o Zabbix Agent

/etc/init.d/zabbix-agent restart
