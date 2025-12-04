# 🩺 Internet das Coisas na Saúde: Monitoramento de Sinais Vitais com ESP32 e MQTT (ODS 3)

## 💡 1. Visão Geral do Projeto

Este projeto é um protótipo de Internet das Coisas (IoT) de baixo custo desenvolvido para monitorar sinais vitais (temperatura e batimentos cardíacos simulados) utilizando o microcontrolador ESP32. Os dados são processados localmente e enviados em tempo real para um broker MQTT público, permitindo a visualização remota e acionamento de alertas imediatos.

O trabalho está alinhado com o **Objetivo de Desenvolvimento Sustentável (ODS) 3 da ONU**, focado em promover saúde e bem-estar para todos.

## ✨ 2. Funcionalidades

O protótipo realiza as seguintes ações de forma contínua:

* **Monitoramento de Temperatura:** Leitura do sensor digital DS18B20.
* **Simulação de BPM:** Geração de Batimentos Cardíacos por Minuto (BPM) via software (`random()`) entre 60 e 139 BPM, para fins de teste de eventos.
* **Comunicação em Nuvem:** Envio de dados em formato JSON via protocolo MQTT.
* **Alerta Local:** Acionamento de alerta sonoro (Buzzer no GPIO 13) quando:
    * Temperatura 38.0 Graus **OU**
    * BPM 120
* **Visualização Remota:** Dados recebidos no aplicativo móvel MQTT Dashboard.

## 🛠️ 3. Arquitetura e Componentes

| Componente | Função | Conexão Principal com ESP32 |
| :--- | :--- | :--- |
| **ESP32 DevKit V4** | Microcontrolador principal (Wi-Fi integrado) | - |
| **DS18B20** | Sensor Digital de Temperatura | GPIO 4 (OneWire) |
| **Buzzer Piezoelétrico** | Atuador de Alerta Sonoro | GPIO 13 |
| **Potenciômetro** | Entrada Analógica (ADC) - *Incluído no diagrama, mas não utilizado para leitura de BPM no código final.* | GPIO 34 |
| **Resistor** | Resistor pull-up de 4.7kΩ | Linha de dados do DS18B20 |

### 3.1. Diagrama de Conexão (Fritzing)

<img width="1090" height="905" alt="Diagrama Fritizing" src="https://github.com/user-attachments/assets/db6f42f0-4104-4a3f-a10f-50ebc18681e6" />

## ☁️ 4. Configuração de Comunicação (MQTT)

O sistema utiliza o protocolo MQTT, conhecido por sua eficiência e baixa latência em IoT.

* **Broker Público:** `broker.hivemq.com`
* **Porta:** `1883`
* **Tópico de Publicação:** `projeto/ods3/dados`
* **Exemplo de Payload JSON Publicado:**
    ```json
    {"temp": 36.50, "bpm": 128, "status": "Alerta!"}
    ```

## ⚙️ 5. Como Rodar (Setup)

O projeto pode ser executado facilmente na simulação online ou em hardware físico:

### 5.1. Execução no Ambiente de Simulação (Wokwi)

Se você estiver rodando o projeto diretamente no Wokwi, **nenhuma instalação é necessária**, pois o ambiente já fornece a plataforma ESP32 e todas as bibliotecas.

### 5.2. Execução em Hardware Físico (Placa ESP32 Real)

Para compilar e carregar o código em uma placa ESP32 real usando a Arduino IDE, você deve instalar os pré-requisitos:

1.  **Instale a plataforma ESP32** no Gerenciador de Placas da Arduino IDE.
2.  **Instale as seguintes bibliotecas** via Gerenciador de Bibliotecas:
    * `PubSubClient` (Para comunicação MQTT)
    * `OneWire` (Requisito para o DS18B20)
    * `DallasTemperature` (Para leitura do DS18B20)

### 5.3. Credenciais Wi-Fi

O projeto está configurado para a rede de simulação Wokwi. Para utilizar em sua rede Wi-Fi local, edite o código no início do arquivo `.ino` com suas credenciais:

```cpp
const char* ssid = "Sua_Rede_WiFi_Aqui";
const char* password = "Sua_Senha_Aqui";

Entendido. Para garantir que o seu README.md esteja 100% correto e claro, removendo qualquer ambiguidade sobre o que precisa ser instalado para a simulação online versus o hardware físico.

Aqui está o conteúdo completo da Seção 5, que você pode usar para substituir o bloco anterior no seu README.md:

⚙️ 5. Como Rodar (Setup) - CORRETO
Markdown

## ⚙️ 5. Como Rodar (Setup)

O projeto pode ser executado facilmente na simulação online ou em hardware físico:

### 5.1. Execução no Ambiente de Simulação (Wokwi)

Se você estiver rodando o projeto diretamente no Wokwi, **nenhuma instalação é necessária**, pois o ambiente já fornece a plataforma ESP32 e todas as bibliotecas.

### 5.2. Execução em Hardware Físico (Placa ESP32 Real)

Para compilar e carregar o código em uma placa ESP32 real usando a Arduino IDE, você deve instalar os pré-requisitos:

1.  **Instale a plataforma ESP32** no Gerenciador de Placas da Arduino IDE.
2.  **Instale as seguintes bibliotecas** via Gerenciador de Bibliotecas:
    * `PubSubClient` (Para comunicação MQTT)
    * `OneWire` (Requisito para o DS18B20)
    * `DallasTemperature` (Para leitura do DS18B20)

### 5.3. Credenciais Wi-Fi

O projeto está configurado para a rede de simulação Wokwi. Para utilizar em sua rede Wi-Fi local, edite o código no início do arquivo `.ino` com suas credenciais:

```cpp
const char* ssid = "Sua_Rede_WiFi_Aqui";
const char* password = "Sua_Senha_Aqui";
5.4. Visualização (MQTT Dashboard)
Configure o aplicativo MQTT Dashboard (ou similar) no seu dispositivo móvel para se conectar ao broker broker.hivemq.com e assinar o tópico projeto/ods3/dados para visualizar os dados em tempo real.
