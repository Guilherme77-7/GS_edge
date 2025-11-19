<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<div align="center">

# 🍅 ESP32 IoT Pomodoro Timer

![C++](https://img.shields.io/badge/Language-C%2B%2B-00599C?style=for-the-badge&logo=c%2B%2B)
![ESP32](https://img.shields.io/badge/Hardware-ESP32-red?style=for-the-badge&logo=espressif)
![Wokwi](https://img.shields.io/badge/Simulador-Wokwi-blue?style=for-the-badge)
![MQTT](https://img.shields.io/badge/Protocol-MQTT-orange?style=for-the-badge)
![Node-RED](https://img.shields.io/badge/Backend-Node--RED-8F0000?style=for-the-badge&logo=nodered)

**Um timer de produtividade inteligente conectado à nuvem, com feedback visual imersivo via OLED e LEDs NeoPixel.**

<br>

<img width="900" alt="Circuito Wokwi ESP32 Pomodoro" src="https://github.com/user-attachments/assets/ac507d1c-b8f8-45d9-a6ba-7fb1fd5b6df8" />

</div>
</head>
<body>

<div class="center">
  <h1>🍅 ESP32 IoT Pomodoro Timer</h1>
  <div class="badge">
    <img src="https://img.shields.io/badge/Language-C%2B%2B-00599C?style=for-the-badge&logo=c%2B%2B" alt="C++">
  </div>
  <div class="badge">
    <img src="https://img.shields.io/badge/Hardware-ESP32-red?style=for-the-badge&logo=espressif" alt="ESP32">
  </div>
  <div class="badge">
    <img src="https://img.shields.io/badge/Simulador-Wokwi-blue?style=for-the-badge" alt="Wokwi">
  </div>
  <div class="badge">
    <img src="https://img.shields.io/badge/Protocol-MQTT-orange?style=for-the-badge" alt="MQTT">
  </div>
  <div class="badge">
    <img src="https://img.shields.io/badge/Backend-Node--RED-8F0000?style=for-the-badge&logo=nodered" alt="Node-RED">
  </div>
  <p><strong>Um timer de produtividade inteligente conectado à nuvem, com feedback visual imersivo via OLED e LEDs NeoPixel.</strong></p>
</div>

<hr>

<h2>📖 Sobre o Projeto</h2>
<p>Este projeto visa criar uma ferramenta de auxílio ao foco utilizando a técnica <strong>Pomodoro</strong>. Diferente de timers comuns, este dispositivo oferece uma experiência visual rica e conectividade IoT total. O sistema permite monitoramento remoto em tempo real através de um Dashboard interativo, utilizando o protocolo MQTT para comunicação de baixa latência.</p>

<h3>✨ Funcionalidades Principais</h3>
<ul>
  <li><strong>Display OLED:</strong> Feedback imediato do status (Foco, Pausa, Contagem).</li>
  <li><strong>Feedback Luminoso (NeoPixel):</strong>
    <ul>
      <li>🔴 <strong>Vermelho:</strong> Modo Foco (Trabalhando).</li>
      <li>🟡 <strong>Amarelo:</strong> Pausado.</li>
      <li>🔵 <strong>Azul:</strong> Finalizado (Descanso).</li>
      <li>⚫ <strong>Cinza/Off:</strong> Desconectado ou Parado.</li>
    </ul>
  </li>
  <li><strong>Controle Físico:</strong> Navegação intuitiva via Joystick analógico.</li>
  <li><strong>Conectividade IoT:</strong> Sincronização bidirecional com a nuvem.</li>
  <li><strong>Dashboard Inteligente:</strong> Visualização gráfica de estatísticas e status via Node-RED.</li>
</ul>
<img width="1904" height="933" alt="{443DA993-D79F-41A6-8606-8CD4D6B45779}" src="https://github.com/user-attachments/assets/51546246-dd6d-40f2-841c-805b5b2d7492" />

<hr>

<h2>🏗️ Arquitetura do Sistema</h2>
<p>O projeto utiliza uma arquitetura <strong>Publish-Subscribe (Pub/Sub)</strong> baseada em MQTT para desacoplar o hardware (ESP32) da interface de usuário (Node-RED).</p>

<h3>Componentes da Arquitetura:</h3>
<ul>
  <li><strong>Borda (Edge):</strong> O ESP32 gerencia a lógica de tempo, leitura de sensores e feedback visual.</li>
  <li><strong>Transporte:</strong> Os estados (start, stop, offline, etc.) são enviados via Wi-Fi para o Broker MQTT Público.</li>
  <li><strong>Backend/Frontend:</strong> O Node-RED processa as mensagens, calcula estatísticas de produtividade e renderiza o Dashboard.</li>
</ul>

<hr>

<h2>🛠️ Hardware Necessário</h2>
<table>
  <tr>
    <th>Componente</th>
    <th>Quantidade</th>
    <th>Detalhes Técnicos</th>
  </tr>
  <tr>
    <td>ESP32 DevKit V1</td>
    <td>1</td>
    <td>Microcontrolador Dual Core + Wi-Fi</td>
  </tr>
  <tr>
    <td>Display OLED</td>
    <td>1</td>
    <td>SSD1306 (128x64) Interface I2C</td>
  </tr>
  <tr>
    <td>NeoPixel Ring</td>
    <td>1</td>
    <td>Anel de 16 LEDs RGB Endereçáveis</td>
  </tr>
  <tr>
    <td>Joystick Analógico</td>
    <td>1</td>
    <td>Módulo KY-023 (Eixos X/Y + Switch)</td>
  </tr>
</table>

<hr>

<h2>🔌 Pinout (Mapa de Conexões)</h2>
<p>Configuração física utilizada no simulador e no código (<code>sketch.ino</code>).</p>
<table>
  <tr>
    <th>Componente</th>
    <th>Pino Físico</th>
    <th>GPIO ESP32</th>
    <th>Função</th>
  </tr>
  <tr>
    <td>OLED</td>
    <td>SDA</td>
    <td>GPIO 21</td>
    <td>Dados I2C</td>
  </tr>
  <tr>
    <td>OLED</td>
    <td>SCL</td>
    <td>GPIO 22</td>
    <td>Clock I2C</td>
  </tr>
  <tr>
    <td>NeoPixel</td>
    <td>DIN</td>
    <td>GPIO 5</td>
    <td>Sinal de Controle LED</td>
  </tr>
  <tr>
    <td>Joystick</td>
    <td>VRy (Vertical)</td>
    <td>GPIO 34</td>
    <td>Eixo Y (Start/Pause)</td>
  </tr>
  <tr>
    <td>Joystick</td>
    <td>VRx (Horizontal)</td>
    <td>GPIO 35</td>
    <td>Eixo X (Stop/Resume)</td>
  </tr>
  <tr>
    <td>Joystick</td>
    <td>SW (Button)</td>
    <td>GPIO 25</td>
    <td>Botão de Seleção</td>
  </tr>
</table>

<hr>

<h2>🚀 Guia Passo a Passo de Execução</h2>
<p>Para rodar este projeto, você precisará de duas partes funcionando simultaneamente: o Hardware (Simulado) e o Dashboard.</p>

<h3>Passo 1: Configurar o Hardware (Wokwi)</h3>
<ol>
  <li>Acesse o <a href="https://wokwi.com" target="_blank">Wokwi.com</a></li>
  <li>Crie um novo projeto escolhendo a placa <strong>ESP32</strong></li>
  <li>No arquivo <code>sketch.ino</code>, cole o código C++ disponível na pasta <code>/src</code> deste repositório</li>
  <li>No arquivo <code>diagram.json</code>, copie a configuração de conexões</li>
  <li>Adicione as seguintes bibliotecas no gerenciador (<code>libraries.txt</code>):
    <ul>
      <li>Adafruit GFX Library</li>
      <li>Adafruit SSD1306</li>
      <li>Adafruit NeoPixel</li>
      <li>PubSubClient</li>
    </ul>
  </li>
</ol>

<h3>Passo 2: Configurar o Dashboard (Node-RED)</h3>
<ol>
  <li>Certifique-se de ter o <strong>Node.js</strong> instalado no seu computador</li>
  <li>Instale o Node-RED via terminal:
    <pre>npm install -g --unsafe-perm node-red</pre>
  </li>
  <li>Instale o pacote de Dashboard:
    <ul>
      <li>Abra o Node-RED</li>
      <li>Vá em <strong>Menu > Manage Palette > Install</strong></li>
      <li>Busque por <code>node-red-dashboard</code></li>
    </ul>
  </li>
  <li>Importe o Fluxo:
    <ul>
      <li>Vá em <strong>Menu > Import</strong></li>
      <li>Selecione o arquivo <code>dashboard_pomodoro.json</code> deste repositório</li>
      <li>Clique em <strong>Deploy</strong> (canto superior direito)</li>
    </ul>
  </li>
</ol>

<h3>Passo 3: Rodar e Testar</h3>
<ol>
  <li>No Wokwi, clique no botão <strong>Play</strong> (Verde)</li>
  <li>No seu navegador, acesse o Dashboard local:
    <pre>http://localhost:1880/ui</pre>
  </li>
  <li>Utilize o Joystick no Wokwi e observe a mágica acontecer no Dashboard em tempo real!</li>
</ol>

<hr>

<h2>🎮 Manual de Operação</h2>
<p>O controle do sistema é centralizado no Joystick para evitar múltiplos botões.</p>
<table>
  <tr>
    <th>Ação no Joystick</th>
    <th>Comando</th>
    <th>Descrição</th>
  </tr>
  <tr>
    <td>⬆️ Cima</td>
    <td>START</td>
    <td>Inicia o cronômetro (LED Vermelho)</td>
  </tr>
  <tr>
    <td>⬇️ Baixo</td>
    <td>PAUSE</td>
    <td>Pausa a contagem (LED Amarelo)</td>
  </tr>
  <tr>
    <td>➡️ Direita</td>
    <td>RESUME</td>
    <td>Retoma de onde parou</td>
  </tr>
  <tr>
    <td>⬅️ Esquerda</td>
    <td>STOP</td>
    <td>Para e reseta o tempo e estatísticas</td>
  </tr>
</table>

<hr>

<h2>☁️ Configuração MQTT</h2>
<p>O sistema já vem pré-configurado para uso imediato em testes.</p>
<ul>
  <li><strong>Broker:</strong> <code>test.mosquitto.org</code> (Público)</li>
  <li><strong>Porta:</strong> <code>1883</code></li>
  <li><strong>Tópico Principal:</strong> <code>pomodoro/status</code></li>
</ul>

<h3>Nota Técnica</h3>
<p>O sistema implementa <strong>LWT (Last Will and Testament)</strong>. Se o ESP32 perder energia ou conexão, o Broker avisa o Dashboard enviando o payload <code>offline</code> automaticamente.</p>

<hr>

<h2>📁 Estrutura do Repositório</h2>
<pre>esp32-pomodoro-timer/
├── src/
│   ├── sketch.ino
│   └── config.h
├── node-red/
│   └── dashboard_pomodoro.json
├── wokwi/
│   ├── diagram.json
│   └── libraries.txt
├── docs/
│   └── ARQUITETURA.md
├── README.md
└── LICENSE</pre>

<hr>

<h2>📊 Tópicos MQTT</h2>

<h3>Publicados pelo ESP32</h3>
<pre>{
  "status": "running|paused|stopped|offline",
  "time_remaining": 1234,
  "session_count": 5,
  "total_focus_time": 3600,
  "timestamp": "2024-01-15T10:30:00Z"
}</pre>

<h3>Inscritos pelo ESP32</h3>
<pre>{
  "command": "start|pause|resume|stop",
  "settings": {
    "work_duration": 1500,
    "break_duration": 300
  }
}</pre>

<hr>

<h2>🔐 Segurança e Privacidade</h2>
<ul>
  <li>O Broker MQTT utilizado é <strong>público e sem autenticação</strong> para fins de demonstração</li>
  <li>Para uso em produção, configure um Broker privado com autenticação TLS/SSL</li>
  <li>Nunca compartilhe credenciais Wi-Fi no controle de versão</li>
</ul>

<hr>

<h2>🐛 Troubleshooting</h2>

<h3>ESP32 não conecta ao Wi-Fi</h3>
<ul>
  <li>Verifique as credenciais no <code>config.h</code></li>
  <li>Certifique-se de que o 2.4GHz está habilitado no seu roteador</li>
</ul>

<h3>Dashboard não atualiza em tempo real</h3>
<ul>
  <li>Verifique se o Broker MQTT está acessível</li>
  <li>Use <code>mosquitto_sub -h test.mosquitto.org -t "pomodoro/#"</code> para debugar</li>
</ul>

<h3>Display OLED não liga</h3>
<ul>
  <li>Verifique a conexão I2C nos pinos 21 e 22</li>
  <li>Teste o endereço I2C: <code>0x3C</code> é o padrão</li>
</ul>

<hr>

<h2>📚 Referências e Recursos</h2>
<ul>
  <li><a href="https://docs.espressif.com/projects/esp-idf/en/latest/esp32/" target="_blank">Documentação ESP32</a></li>
  <li><a href="https://github.com/knolleary/pubsubclient" target="_blank">PubSubClient Library</a></li>
  <li><a href="https://nodered.org/docs/" target="_blank">Node-RED Official Docs</a></li>
  <li><a href="https://en.wikipedia.org/wiki/Pomodoro_Technique" target="_blank">Técnica Pomodoro</a></li>
  <li><a href="https://wokwi.com" target="_blank">Wokwi Simulator</a></li>
</ul>

<hr>

<h2>👨‍💼 Autor</h2>
<p>Desenvolvido para fins acadêmicos - <strong>Engenharia de Software</strong></p>

<hr>

<h2>📄 Licença</h2>
<p>Este projeto está licenciado sob a <strong>MIT License</strong> - veja o arquivo <code>LICENSE</code> para detalhes.</p>

<hr>

<h2>🤝 Contribuições</h2>
<p>Contribuições são bem-vindas! Abra uma <strong>Issue</strong> ou envie um <strong>Pull Request</strong> com melhorias, correções de bugs ou novas funcionalidades.</p>

<hr>

<h2>💡 Roadmap Futuro</h2>
<ul>
  <li>☐ Suporte a múltiplos timers sincronizados</li>
  <li>☐ Integração com Google Calendar</li>
  <li>☐ Análise de produtividade com IA</li>
  <li>☐ App mobile nativa (React Native)</li>
  <li>☐ Modo offline com sincronização posterior</li>
  <li>☐ Histórico de sessões persistente</li>
</ul>

<hr>

<div class="center">
  <p><strong>⭐ Se este projeto foi útil para você, considere deixar uma estrela no GitHub!</strong></p>
</div>

</body>
</html>
