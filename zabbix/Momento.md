# Medir o minuto e segundo

## Fazer Script para informar o tempo MM.SS
cd /usr/lib/zabbix/externalscripts

nano contador.sh

### escrever o seguinte codigo
\#! /bin/bash

segundos=`date +%s`

tempo=`date -d @$segundos +%M.%S`

echo "$tempo"

### estabelecer permissões

chmod 777 contador.sh
