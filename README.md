<div align="center">

# 🍅 ESP32 IoT Pomodoro Timer

![C++](https://img.shields.io/badge/Language-C%2B%2B-00599C?style=for-the-badge&logo=c%2B%2B)
![ESP32](https://img.shields.io/badge/Hardware-ESP32-red?style=for-the-badge&logo=espressif)
![Wokwi](https://img.shields.io/badge/Simulador-Wokwi-blue?style=for-the-badge)
![MQTT](https://img.shields.io/badge/Protocol-MQTT-orange?style=for-the-badge)

**Um timer de produtividade inteligente conectado à nuvem, com feedback visual imersivo via OLED e LEDs NeoPixel.**

</div>

---<img width="1900" height="519" alt="{09AE2E98-23CB-42A9-B113-DFEFECC3FF2A}" src="https://github.com/user-attachments/assets/ac507d1c-b8f8-45d9-a6ba-7fb1fd5b6df8" />


## 📖 Sobre o Projeto

Este projeto visa criar uma ferramenta de auxílio ao foco utilizando a técnica **Pomodoro**. Diferente de timers comuns, este dispositivo oferece uma experiência visual rica e conectividade IoT, permitindo que o status de "Foco" ou "Pausa" seja monitorado remotamente ou gatilhe automações residenciais (como mudar a cor das luzes do quarto ou silenciar notificações).

### ✨ Funcionalidades
- **Display OLED:** Mostra o status atual (Foco, Pausa, Parado) e a contagem regressiva.
- **Anel de LEDs (NeoPixel):** Feedback luminoso colorido intuitivo.
    - 🔴 **Vermelho:** Em foco (trabalhando).
    - 🟡 **Amarelo:** Pausado.
    - 🔵 **Azul:** Finalizado (Hora do descanso).
- **Controle via Joystick:** Navegação física tátil sem necessidade de botões complexos.
- **Integração MQTT:** Envia o status em tempo real para um broker, permitindo integração com **Node-RED**, **Home Assistant** ou Dashboards personalizados.

---

## 🛠️ Hardware Necessário

| Componente | Quantidade | Descrição |
| :--- | :---: | :--- |
| **ESP32 DevKit V1** | 1 | Microcontrolador com Wi-Fi |
| **Display OLED** | 1 | SSD1306 (128x64) I2C |
| **NeoPixel Ring** | 1 | Anel de 16 LEDs RGB |
| **Joystick Analógico** | 1 | Módulo padrão (KY-023) |

---

## 🔌 Esquema de Ligação (Pinout)

As conexões abaixo correspondem à configuração padrão do código (`sketch.ino`).

| Componente | Pino Físico | ESP32 GPIO |
| :--- | :--- | :--- |
| **OLED** | SDA | `21` |
| | SCL | `22` |
| **NeoPixel** | DIN (Data) | `5` |
| **Joystick** | VRy (Vertical) | `34` |
| | VRx (Horizontal)| `35` |
| | SW (Botão) | `25` |

> **Nota:** Todos os componentes compartilham o **GND**. O OLED e Joystick usam **3.3V**, e o NeoPixel geralmente usa **5V** (embora funcione com 3.3V em alguns casos).

---

## 🎮 Guia de Operação

O controle é feito inteiramente pelo Joystick:

| Ação no Joystick | Função | Estado Necessário |
| :--- | :--- | :--- |
| **Pressionar (Click)** | `Start` / `Pause` / `Resume` | Qualquer (Contextual) |
| **Cima (Eixo Y)** | `Start` (Iniciar) | Parado |
| **Baixo (Eixo Y)** | `Pause` (Pausar) | Rodando |
| **Direita (Eixo X)** | `Resume` (Retomar) | Pausado |
| **Esquerda (Eixo X)** | `Stop` (Parar/Resetar) | Qualquer |

---

## ☁️ Configuração MQTT

O dispositivo se conecta ao Wi-Fi e publica mensagens no tópico configurado.

- **Broker Público:** `test.mosquitto.org`
- **Porta:** `1883`
- **Tópico:** `pomodoro/status`

**Payloads enviados:**
- `start`
- `pause`
- `resume`
- `stop`
- `finished`

---

## 🚀 Como Executar (Simulador Wokwi)

1. Acesse [Wokwi.com](https://wokwi.com).
2. Crie um novo projeto para **ESP32**.
3. Cole o código do `sketch.ino`.
4. Adicione os arquivos `diagram.json` e `libraries.txt` (lista abaixo).
5. Inicie a simulação.

### Dependências (`libraries.txt`)
```text
Adafruit GFX Library
Adafruit SSD1306
Adafruit NeoPixel
PubSubClient
