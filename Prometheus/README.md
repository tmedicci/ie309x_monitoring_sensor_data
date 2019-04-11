# Prometheus

O estudo desta solução de monitoramento é baseada na própria documentação disponível no [site oficial](https://prometheus.io/docs/introduction/overview/) e em outros tutoriais disponíveis.

## Impressões Iniciais
Boa parte dos tutorias disponíveis utilizam containers (docker) para desenvolver as aplicações do servidor, da visualização (normalmente integrada ao Grafana) e dos targets (agentes que enviam dados de série temportal).

## Submódulos utilizados:
* [client_golang](https://prometheus.io/docs/prometheus/latest/getting_started/) do exemplo desenvolvido na documentação oficial.
* [Tutorial do Medium - Monitorando a saúde de sua aplicação](https://medium.com/tech-grupozap/prometheus-monitorando-a-sa%C3%BAde-da-sua-aplica%C3%A7%C3%A3o-bd9b3b63e7b1), que provê um ambiente docker completo e uma aplicação exemplo.

## Próximas Etapas

### Utilizando o Exemplo com Containers
1. Investigar o monitoramento dos ciclos de escrita em disco para uma pasta específica:
 * Investigar volumes do docker (mount point);
 * Investigar se é possível montar este volume para monitorá-lo a partir do node exporter (diskstat)
2. Realizar um teste inicial de ciclos de escrita destativando os demais targets (inclusive collectors não usados no node exporter)
3. Entender o funcionamento do Grafana.