# Intro-o-AWS-IoT-protocolo-MQTT
Repositorio destinado ao projeto de extensão sobre serviços AWS IoT . Utilizando como exemplo um código sobre o protocolo MQTT.

# Projeto: Conexão MQTT em Python com AWS IoT Core

## Introdução

Este projeto tem como objetivo estabelecer uma conexão entre um dispositivo local e a nuvem da AWS usando o protocolo MQTT (Message Queuing Telemetry Transport). A comunicação MQTT é leve e eficiente, ideal para aplicações de Internet das Coisas (IoT). Utilizaremos o AWS IoT Core como o serviço de gerenciamento de dispositivos e a biblioteca Python `paho-mqtt` para implementar a conexão MQTT.

## Objetivos

1. Estabelecer uma conexão segura MQTT entre um dispositivo local e o AWS IoT Core.
2. Publicar e assinar mensagens em um tópico MQTT na AWS.
3. Gerenciar as credenciais de segurança e a configuração do dispositivo na AWS.
4. Monitorar e testar a comunicação através do console da AWS.

## Pré-requisitos

- Conta AWS ativa.
- Python 3.x instalado.
- Bibliotecas Python: `paho-mqtt`, `AWSIoTPythonSDK`.
- Certificados de segurança (chave privada, certificado do cliente, certificado da CA) fornecidos pelo AWS IoT Core.

## Configuração do AWS IoT Core

### 1. Criar um "thing" na AWS IoT

1. Acesse o console AWS IoT Core.
2. Navegue até "Manage" > "Things" e clique em "Create".
3. Siga as etapas para criar um novo "thing" e baixar os certificados de segurança (chave privada, certificado do cliente e certificado da CA). 

### 2. Configurar uma política IoT

1. Em "Secure" > "Policies", crie uma nova política IoT que permita ao dispositivo publicar e assinar em tópicos específicos.
2. Conceda permissões adequadas, por exemplo:
    ```json
    {
      "Version": "2012-10-17",
      "Statement": [
        {
          "Effect": "Allow",
          "Action": [
            "iot:Publish",
            "iot:Subscribe",
            "iot:Connect",
            "iot:Receive"
          ],
          "Resource": "arn:aws:iot:<region>:<account-id>:topic/*"
        }
      ]
    }
    ```

### 3. Atribuir a política ao "thing"

1. Navegue até o seu "thing".
2. Vincule os certificados e a política criada anteriormente.

## Configuração do Cliente Python

### 1. Instalar bibliotecas necessárias

Execute o seguinte comando para instalar a biblioteca `AWSIoTPythonSDK`:

```bash
pip install AWSIoTPythonSDK
```

### 2. Script Python para Conexão MQTT

Abaixo está um exemplo de script em Python para conectar ao AWS IoT Core usando MQTT:

```python
from AWSIoTPythonSDK.MQTTLib import AWSIoTMQTTClient

# Configurações do AWS IoT
client_id = "meuDispositivo"
endpoint = "seu-endpoint-ats.iot.<regiao>.amazonaws.com"
root_ca = "caminho/para/AmazonRootCA1.pem"
private_key = "caminho/para/seu-certificado-private.pem.key"
cert = "caminho/para/seu-certificado.pem.crt"
topic = "meu/topico/mqtt"

# Inicializar o cliente MQTT
mqtt_client = AWSIoTMQTTClient(client_id)
mqtt_client.configureEndpoint(endpoint, 8883)
mqtt_client.configureCredentials(root_ca, private_key, cert)

# Configurações adicionais do MQTT
mqtt_client.configureOfflinePublishQueueing(-1)  # Fila de mensagens offline ilimitada
mqtt_client.configureDrainingFrequency(2)  # Processa 2 mensagens/segundo ao reconectar
mqtt_client.configureConnectDisconnectTimeout(10)  # Timeout para conectar/desconectar
mqtt_client.configureMQTTOperationTimeout(5)  # Timeout para operações MQTT (publicar, assinar, etc.)

# Função de callback para mensagens recebidas
def custom_callback(client, userdata, message):
    print(f"Mensagem recebida: {message.payload} de {message.topic}")

# Conectar ao AWS IoT Core
mqtt_client.connect()

# Inscrever-se no tópico
mqtt_client.subscribe(topic, 1, custom_callback)

# Publicar uma mensagem
mqtt_client.publish(topic, "Hello from Python!", 1)

# Manter o script rodando
import time
while True:
    time.sleep(1)
```

### 3. Executar o Script

Certifique-se de que os caminhos para os certificados (`root_ca`, `private_key` e `cert`) estejam corretos no script. Execute o script:

```bash
python seu_script.py
```

## Testando a Conexão

1. Acesse o console do AWS IoT Core.
2. Navegue até "Test" e inscreva-se no tópico usado no script.
3. Verifique se as mensagens publicadas aparecem no console.

## Conclusão

Este projeto demonstrou como configurar uma conexão MQTT entre um dispositivo local e o AWS IoT Core usando Python. Através do protocolo MQTT e da infraestrutura de segurança da AWS, conseguimos estabelecer uma comunicação segura e eficiente para aplicações IoT.

## Próximos Passos

- Implementar lógica adicional para processar mensagens.
- Expandir o projeto para múltiplos dispositivos.
- Integrar a comunicação MQTT com outros serviços da AWS, como Lambda, DynamoDB, etc.

## Referências

- [Documentação AWS IoT Core](https://docs.aws.amazon.com/iot/latest/developerguide/what-is-aws-iot.html)
- [Biblioteca AWSIoTPythonSDK](https://github.com/aws/aws-iot-device-sdk-python)
