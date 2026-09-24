# ThermoTrack — Firmware

Firmware para **ESP32** do **ThermoTrack**, uma caixa de transporte inteligente que monitora **temperatura, umidade, movimento e localização** e envia os dados em tempo real via **MQTT**.

> O código focado apenas no módulo GPS está em [GPSThermoTrack](https://github.com/LeonardoFuents/GPSThermoTrack).

## O que ele faz

- Lê **temperatura e umidade** com o sensor **DHT22**
- Detecta **movimento/impacto** com o acelerômetro **MMA8452Q**
- Obtém **latitude e longitude** pelo módulo **SIM808** (GPS)
- Publica tudo em JSON no tópico MQTT `trackbox/sensores`
- Recebe comandos pelo MQTT (estado de **trava** e **alertas**)

Exemplo de mensagem publicada:

```json
{
  "temperatura": 24.5,
  "umidade": 60.1,
  "movimento": false,
  "latitude": -23.55,
  "longitude": -46.63,
  "trava": true,
  "alerta": false
}
```

## Hardware

| Componente | Ligação |
|---|---|
| ESP32 DevKit | — |
| DHT22 | GPIO 4 |
| SIM808 (GPS) | RX 16 / TX 17 |
| MMA8452Q | I2C |

## Tecnologias

- C++ / Arduino framework
- [PlatformIO](https://platformio.org/)
- Bibliotecas: PubSubClient (MQTT), ArduinoJson, DHT sensor library, SparkFun MMA8452Q

## Como compilar

1. Instale o VS Code com a extensão **PlatformIO**.
2. Preencha o Wi-Fi em `include/senhas.h` (`SSID` e `SENHA`).
3. Compile e grave no ESP32:

```bash
pio run --target upload
pio device monitor -b 115200
```

## Autor

**Leonardo Fuentes** — [GitHub](https://github.com/LeonardoFuents)
