# Monitoraramento do Ambiente da Cidade de Campinas-SP

## Instalar aplicação linx
sudo apt-get install lynx

## Mostrar Temperatura e Sensação Térmica apresentada no site usando a aplicação lins
### acessando o site sensação térmica
#### Temperatura
lynx -dump https://www.sensacaotermica.com.br/campinas-sp/ | grep Temperatura: | sed 's/º//g' | awk '{print $2}'
#### Sensação térmica
lynx -dump https://www.sensacaotermica.com.br/campinas-sp/ | grep Térmica: | sed 's/º//g' | awk '{print $3}'

### acessando o clima tempo
#### Temperatura C
lynx -dump https://www.climatempo.com.br/previsao-do-tempo/cidade/418/campinas-sp | grep -B 6 'Vento:' | head -1 | sed 's/°//g' | awk '{print $1}'
#### Sensação C
lynx -dump https://www.climatempo.com.br/previsao-do-tempo/cidade/418/campinas-sp | grep -A 2 'Vento:' | tail -n 1 | awk '{print $2}' | sed 's/°//g'
#### umidade %
lynx -dump https://www.climatempo.com.br/previsao-do-tempo/cidade/418/campinas-sp | grep -A 3 'Vento:' | tail -n 1 | awk '{print $2}' | sed 's/%//g'
#### pressao hPa
lynx -dump https://www.climatempo.com.br/previsao-do-tempo/cidade/418/campinas-sp | grep -A 4 'Vento:' | tail -n 1 | awk '{print $2}'


## Editar Configuração do Zabbix Agent
sudo nano /etc/zabbix/zabbix_agentd.conf

### Editar a opção Parametro de usuário (Option: UserParameter)

#### site Sensação térmica
UserParameter=STTemperatura,lynx -dump https://www.sensacaotermica.com.br/campinas-sp/ | grep Temperatura: | sed 's/º//g' | awk '{print $2}'

UserParameter=STSensacao,lynx -dump https://www.sensacaotermica.com.br/campinas-sp/ | grep Térmica: | sed 's/º//g' | awk '{print $3}'

#### site clima tempo
UserParameter=CTTemperatura,lynx -dump https://www.climatempo.com.br/previsao-do-tempo/cidade/418/campinas-sp | grep -B 6 'Vento:' | head -1 | sed 's/°//g' | awk '{print $1}'

UserParameter=CTSensacao,lynx -dump https://www.climatempo.com.br/previsao-do-tempo/cidade/418/campinas-sp | grep -A 2 'Vento:' | tail -n 1 | awk '{print $2}' | sed 's/°//g'

UserParameter=CTumidade,lynx -dump https://www.climatempo.com.br/previsao-do-tempo/cidade/418/campinas-sp | grep -A 3 'Vento:' | tail -n 1 | awk '{print $2}' | sed 's/%//g'

UserParameter=CTPressao,lynx -dump https://www.climatempo.com.br/previsao-do-tempo/cidade/418/campinas-sp | grep -A 4 'Vento:' | tail -n 1 | awk '{print $2}'

## Reiniciar o Zabbix Agent

/etc/init.d/zabbix-agent restart

