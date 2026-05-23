# 🐾 Pet Guardian (Smart Pet Dashboard) - IoT & Edge Computing

Um protótipo de "Coleira Inteligente" com foco na saúde e rastreamento de pets, desenvolvido utilizando tecnologias de IoT (Internet of Things) simuladas no ambiente Wokwi. 

## Vídeo IoT:

![Vídeo Youtube](https://youtu.be/H3lOLGCrfb4?si=o1Zv97ZVicVqEamG)


---

## 👥 Integrantes


<table>
<tr>
<th>Nome</th>
<th>RM</th>
<th>Turma</th>
<th>GitHub</th>
<th>LinkedIn</th>
</tr>

<tr>
<td>Enzo Okuizumi</td>
<td>561432</td>
<td>2TDSPG</td>
<td><a href="https://github.com/EnzoOkuizumiFiap">EnzoOkuizumiFiap</a></td>
<td><a href="https://www.linkedin.com/in/enzo-okuizumi-b60292256/">Enzo Okuizumi</a></td>
</tr>

<tr>
<td>Lucas Barros Gouveia</td>
<td>566422</td>
<td>2TDSPG</td>
<td><a href="https://github.com/LuzBGouveia">LuzBGouveia</a></td>
<td><a href="https://www.linkedin.com/in/lucas-barros-gouveia-09b147355/">Lucas Barros Gouveia</a></td>
</tr>

<tr>
<td>Milton Marcelino</td>
<td>564836</td>
<td>2TDSPG</td>
<td><a href="https://github.com/MiltonMarcelino">MiltonMarcelino</a></td>
<td><a href="http://linkedin.com/in/milton-marcelino-250298142">Milton Marcelino</a></td>
</tr>

<tr>
<td>Luna de Carvalho Guimarães</td>
<td>562290</td>
<td>2TDSPG</td>
<td><a href="https://github.com/lunaguima">lunaguima</a></td>
<td><a href="https://www.linkedin.com/in/luna-m-guimar%C3%A3es-1850ab173/">Luna M. Guimarães</a></td>
</tr>

<tr>
<td>Gustavo Okada</td>
<td>563428</td>
<td>2TDSPG</td>
<td><a href="https://github.com/Gdev3356">GustavoOkada7268</a></td>
<td><a href="https://www.linkedin.com/in/gustavo-okada-53a3b8359/">Gustavo Okada</a></td>
</tr>

</table>

---

## 🎯 Objetivos Específicos

### 1. O Problema Real
O projeto busca solucionar a dificuldade de monitorar continuamente a saúde e a localização de animais de estimação. Muitas vezes, os tutores não percebem rapidamente quando o pet está sofrendo de condições graves como hipertermia/insolação, hipotermia, taquicardia ou mesmo quando o animal foge. A falta de informações em tempo real pode resultar em atendimentos veterinários tardios ou na perda do animal.

### 2. Justificativa da Aplicação de IoT
A aplicação de **Internet das Coisas (IoT)** resolve esse problema eliminando a necessidade de supervisão presencial e ininterrupta do dono. Sensores instalados em uma coleira coletam dados vitais e de geolocalização e os transmitem via rede WiFi (protocolo HTTP). Isso permite processar esses dados (Edge Computing no microcontrolador) e disponibilizar um Dashboard dinâmico e em tempo real para os tutores agirem preventivamente diante de emergências. No escopo atual da prova de conceito, mantivemos o foco estrito em conectividade e sensoriamento de hardware (IoT), sem aplicação de Visão Computacional ou IA neste momento.

### 3. Tecnologias Utilizadas e Aplicação
- **Wokwi Simulator:** Ferramenta para desenhar, montar e simular circuitos de IoT.
- **ESP32 (C++ / Arduino Core):** Microcontrolador principal (Cérebro) com WiFi integrado. Coleta dados, realiza análises lógicas e hospeda o servidor web local (Web Server) e a API JSON.
- **Sensor DHT22:** Aplicado para medir a temperatura ambiente próxima ao corpo do animal, garantindo a prevenção contra estresse térmico.
- **Potenciômetro (Simulação de Sensor de Pulso):** Usado na prova de conceito para injetar dados analógicos e simular variações do Batimento Cardíaco (BPM).
- **Módulo GPS (NEO-6M):** Integrado via comunicação Serial (UART) utilizando a biblioteca `TinyGPSPlus` para prover coordenadas geográficas (Lat/Lng) e permitir o rastreamento do animal.
- **Display LCD 16x2 I2C e LEDs:** Utilizados como feedback visual imediato e físico de monitoramento (diretamente na coleira simulada).
- **HTML/CSS/JS e Fetch API:** Front-end embarcado diretamente na memória flash do ESP32, construindo um Dashboard elegante com leitura de dados assíncrona.

### 4. Demonstração de Funcionamento
O sistema opera em um modelo Client-Server (Cliente-Servidor). O ESP32 atua como o servidor na borda. 
- A cada 5 segundos, ele faz a varredura do GPS, Temperatura e BPM.
- **Automação e Regras Lógicas:** O ESP32 analisa localmente se a saúde do pet está em risco. Se a temperatura sair da faixa (36°C a 40°C) ou o BPM sair do aceitável (60 a 160 bpm), o microcontrolador comuta do LED Verde (OK) para o LED Vermelho (Crítico) e atualiza o display LCD exibindo "ALERTA".
- O botão físico do circuito permite alternar a visualização no LCD entre Dados Vitais e Dados de Localização.
- O **Dashboard Web** consome a rota `/api/data` via JavaScript a cada 2 segundos. O front-end reage em tempo real: os cards informativos assumem cores de alarme (bordas e sombras vermelhas, animação de pulso e avisos de "Risco Crítico") automaticamente quando recebem dados fora da janela de normalidade, guiando a atenção do tutor para a urgência.

### 5. Viabilidade Técnica (Prova de Conceito)
A prova de conceito no ambiente simulado foi validada com sucesso, evidenciando total viabilidade técnica para a montagem física no futuro. O ESP32 demonstrou capacidade computacional de sustentar o servidor web (entregando a página e processando dezenas de requisições GET) simultaneamente ao processamento contínuo dos sinais seriais do GPS e dos sinais digitais/analógicos sem apresentar travamentos. A comunicação em tempo real flui perfeitamente estabelecendo um monitoramento sólido.

---

## 🛠️ Organização e Instruções de Uso

### Estrutura do Projeto
- `esp32-server-api/esp32-server-api.ino`: Contém o código-fonte principal em C++ (Lógica de sensoriamento, regras de risco de saúde, servidor HTTP e a página web codificada em Raw String Literal).

### Como Rodar o Protótipo (Simulador Wokwi)
1. Certifique-se de ter todos os componentes (ESP32, DHT22, GPS, Potenciômetro, LCD, LEDs e Botão) montados no arquivo `diagram.json` ou montados fisicamente seguindo a lógica dos pinos.
2. O código requer a instalação das seguintes bibliotecas:
   - `DHT sensor library`
   - `LiquidCrystal I2C`
   - `TinyGPSPlus`
3. Ao iniciar a execução/simulação, o ESP32 conectará no WiFi configurado (`Wokwi-GUEST` no caso do simulador).
4. O sistema exibirá o IP no monitor serial e no LCD (ex: `127.0.0.1:9090` no simulador).
5. Acesse a URL informada no seu navegador web.
6. A página abrirá o "Smart Pet Dashboard" e passará a consumir os dados da API a cada 2 segundos.
7. Altere a temperatura do simulador do DHT22 e o slide do potenciômetro para verificar a automação de risco crítico em ação, acendendo o LED vermelho físico e os alertas no Dashboard.

---

## 📸 Imagens do Projeto

### Wokwi
![Circuito Wokwi](/doc/wokwi-funcionando.png)

### Dashboard
![Dashboard Funcionando](/doc/dashboard-funcionando.png)

---
*Projeto desenvolvido para o 1º Sprint do Challenge Clyvo (Disruptive Architectures, IoT, IOB e IA).*
