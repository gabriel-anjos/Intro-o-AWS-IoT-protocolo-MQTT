# Intro-o-AWS-IoT-protocolo-MQTT
Repositorio destinado ao projeto de extensão sobre serviços AWS IoT . Utilizando como exemplo um código sobre o protocolo MQTT.

## Visão Geral

Este projeto tem como objetivo estabelecer uma conexão segura entre um dispositivo ESP8266 e o serviço AWS IoT Core usando o protocolo MQTT (Message Queuing Telemetry Transport). O ESP8266 atuará como um dispositivo IoT capaz de enviar e receber dados por meio da nuvem, utilizando a infraestrutura oferecida pela Amazon Web Services (AWS).
Objetivos

-Configuração do ESP8266: Programar o ESP8266 para que ele possa se conectar à internet e interagir com o serviço AWS IoT Core.
-Estabelecer Conexão Segura: Implementar uma conexão segura usando certificados SSL/TLS fornecidos pelo AWS IoT Core.
-Comunicação MQTT: Configurar tópicos MQTT para enviar e receber mensagens entre o ESP8266 e o AWS IoT Core.
-Monitoramento e Controle Remoto: Demonstrar como os dados coletados pelo ESP8266 podem ser monitorados e como o dispositivo pode ser controlado remotamente por meio do AWS IoT Core.

## Pré-requisitos
###Hardware

    -ESP8266: Um microcontrolador com capacidade de conexão Wi-Fi.
    -Sensores/Atores: Sensores de temperatura, umidade, etc., conforme a necessidade do projeto.
    -Cabo USB: Para programar o ESP8266 e fornecer energia.

### Software

    -Arduino IDE: Ambiente de desenvolvimento para programar o ESP8266.
    -Bibliotecas Arduino:
        ESP8266WiFi: Para gerenciar a conexão Wi-Fi.
        PubSubClient: Para implementar o protocolo MQTT.
    -AWS Account: Conta na AWS para acessar o AWS IoT Core.
    -AWS CLI: Ferramenta de linha de comando para interagir com os serviços AWS.

## Etapas do Projeto
1. Configuração do Ambiente AWS

    Criar uma Thing no AWS IoT Core:
        Acesse o console do AWS IoT Core.
        Crie uma nova Thing que representará o ESP8266.
        Gere e faça download dos certificados e chaves de segurança.

    Configurar Tópicos MQTT:
        No console do AWS IoT, configure os tópicos MQTT que serão utilizados para comunicação.

    Políticas de Segurança:
        Crie e associe uma política que permita ao dispositivo conectar-se ao AWS IoT Core e publicar/subscrever nos tópicos MQTT.

2. Programação do ESP8266

    Configurar a Conexão Wi-Fi:
        Use a biblioteca ESP8266WiFi para conectar o ESP8266 à rede Wi-Fi local.

    Estabelecer Conexão MQTT:
        Utilize a biblioteca PubSubClient para configurar a conexão MQTT.
        Carregue os certificados SSL/TLS no ESP8266 para autenticação segura.

    Publicar e Subscrever em Tópicos:
        Programe o ESP8266 para publicar dados em um tópico MQTT, como leitura de sensores.
        Configure o ESP8266 para subscrever em tópicos para receber comandos ou atualizações.

3. Testes e Validação

    Monitorar Mensagens no AWS IoT Core:
        Verifique se as mensagens enviadas pelo ESP8266 estão sendo recebidas corretamente no AWS IoT Core.
        Teste o envio de comandos do AWS IoT Core para o ESP8266.

    Validação de Segurança:
        Assegure que a comunicação está sendo feita de forma segura e que o dispositivo está corretamente autenticado.

## Conclusão

Ao final deste projeto, o ESP8266 estará conectado ao AWS IoT Core, enviando e recebendo dados via MQTT de forma segura. Esse tipo de solução é ideal para aplicações em automação residencial, monitoramento ambiental, e outras iniciativas de IoT que necessitem de comunicação eficiente e segura com a nuvem.
Referências

    Documentação Oficial do AWS IoT Core
    ESP8266 Arduino Core
    MQTT Protocol Specification
