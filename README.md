# 🌦️ IoT Weather Dashboard

> Sistema completo de monitorização meteorológica em tempo real com IoT, sensores físicos e interface web responsiva

## 💡 Sobre o Projeto

Uma estação meteorológica inteligente que reúne o melhor de dois mundos: **hardware** (Raspberry Pi, Arduino, sensores) e **software** (plataforma web moderna). 

Imagina teres uma mini-estação meteorológica na tua casa ou escritório, onde podes não só ver a temperatura e humidade em tempo real, mas também controlar dispositivos remotamente, receber alertas, ver gráficos históricos e até capturar fotos do ambiente. Tudo isto acessível de qualquer lugar através do teu browser! 🚀

## ✨ Features

### 📊 **Dashboard em Tempo Real**
Visualiza todos os dados meteorológicos num só lugar, com gráficos bonitos e atualizações automáticas. Sem refreshs chatos!

### 🌡️ **Monitorização de Sensores**
- Temperatura ambiente
- Humidade do ar
- Pressão atmosférica
- E outros sensores personalizados

### 💡 **Controlo Remoto**
Liga e desliga dispositivos à distância através da interface web. LEDs, alarmes, relés - tu mandas!

### 📈 **Histórico Completo**
Vê a evolução dos dados ao longo do tempo. Perfeito para identificar padrões e tendências.

### 📸 **Captura de Imagens**
Tira fotos do ambiente automaticamente e guarda-as para consulta posterior.

### 🔐 **Sistema de Autenticação**
Multi-utilizador com diferentes níveis de acesso. Os teus dados estão seguros!

### 📱 **Design Responsivo**
Funciona perfeitamente em desktop, tablet e smartphone. Monitoriza de onde quiseres!

## 🏗️ Como Funciona?

```
     👤 Utilizador
        │
        │ Acede via Browser
        ▼
   ┌─────────────┐
   │   Web App   │  ← Interface bonita e responsiva
   │  (PHP/HTML) │     com gráficos e controlos
   └──────┬──────┘
          │
          │ API REST
          ▼
   ┌─────────────┐
   │   MySQL     │  ← Guarda todos os dados
   │  Database   │     históricos
   └─────────────┘
          ▲
          │
    ┌─────┴──────┐
    │            │
    ▼            ▼
┌────────┐  ┌─────────┐
│Rasp Pi │  │ Arduino │  ← Recolhem dados dos
│(Python)│  │  (C++)  │     sensores físicos
└───┬────┘  └────┬────┘
    │            │
    ▼            ▼
🌡️ 💧 🔆    💡 🔊 📟  ← Sensores e atuadores
```

**O fluxo é simples:**
1. Sensores captam dados do ambiente (temperatura, humidade, etc)
2. Arduino/Raspberry Pi processam e enviam para o servidor
3. API REST guarda na base de dados
4. Dashboard atualiza automaticamente
5. Tu controlas atuadores remotamente através da web!

## 🛠️ Stack Tecnológica

### 💻 Frontend
```
HTML5 + CSS3 + JavaScript
Bootstrap 5 (design responsivo)
Chart.js (gráficos bonitos)
AJAX (atualizações em tempo real)
```

### ⚙️ Backend
```
PHP 7.4+
MySQL / MariaDB
API REST personalizada
Sistema de autenticação
```

### 🔌 Hardware & IoT
```
🍓 Raspberry Pi 3/4
   └─ Python 3.x
   └─ GPIO control
   └─ Webcam

🤖 Arduino / ESP8266
   └─ C/C++
   └─ Wi-Fi connectivity
   └─ Sensores: DHT22, BMP180, etc.
   └─ Atuadores: LEDs, Relés, Buzzers
```

## 🚀 Quick Start

### Pré-requisitos
- Servidor web (Apache/Nginx)
- PHP 7.4+
- MySQL/MariaDB
- Raspberry Pi com Python 3
- Arduino/ESP8266

### Setup Rápido

```bash
# 1. Clone o repositório
git clone https://github.com/vitorianfonseca/uni-iot-weather-dashboard.git
cd uni-iot-weather-dashboard

# 2. Configure a base de dados
mysql -u root -p < database/schema.sql

# 3. Edite as configurações
nano includes/config.php

# 4. Configure o servidor web para apontar para a pasta do projeto

# 5. Aceda ao projeto
http://localhost/weather-dashboard
```

### 📝 Configuração dos Dispositivos

**Raspberry Pi:**
```bash
cd raspberry_pi/
pip3 install -r requirements.txt
python3 main.py
```

**Arduino/ESP8266:**
1. Abre o Arduino IDE
2. Instala as bibliotecas necessárias (ESP8266WiFi, HTTPClient, ArduinoJson)
3. Configura o Wi-Fi no código
4. Faz upload para a placa

### 🔑 Login Padrão
```
Utilizador: admin
Password: (definida na instalação)
```

## 📁 Estrutura do Projeto

```
📦 uni-iot-weather-dashboard
├── 🌐 Web App
│   ├── index.php              # Página inicial
│   ├── login.php              # Sistema de autenticação
│   ├── dashboard.php          # Dashboard principal
│   ├── history.php            # Visualizar histórico
│   │
│   ├── 📂 api/                # API REST
│   │   ├── sensors.php        # Endpoints dos sensores
│   │   ├── actuators.php      # Controlo de atuadores
│   │   └── images.php         # Upload de imagens
│   │
│   ├── 📂 assets/             # Frontend
│   │   ├── css/               # Estilos personalizados
│   │   ├── js/                # Scripts JavaScript
│   │   └── img/               # Imagens estáticas
│   │
│   └── 📂 includes/           # Backend utilities
│       ├── config.php         # Configurações
│       ├── db.php             # Conexão BD
│       └── functions.php      # Funções auxiliares
│
├── 🍓 Raspberry Pi
│   └── raspberry_pi/
│       ├── main.py            # Script principal
│       ├── sensors.py         # Gestão de sensores
│       └── api_client.py      # Cliente HTTP
│
├── 🤖 Arduino/ESP
│   └── arduino/
│       └── main.ino           # Código para MCU
│
├── 🗄️ Database
│   └── database/
│       └── schema.sql         # Schema da BD
│
└── 📸 Uploads
    └── uploads/               # Imagens da webcam
```

## 📡 API Endpoints

A API REST permite integração fácil com qualquer cliente HTTP:

| Method | Endpoint | Descrição |
|--------|----------|-----------|
| `GET` | `/api/sensors` | Lista todos os sensores ativos |
| `GET` | `/api/sensors/{id}` | Dados de um sensor específico |
| `POST` | `/api/sensors/{id}/data` | Enviar novos dados de sensor |
| `GET` | `/api/actuators` | Lista todos os atuadores |
| `POST` | `/api/actuators/{id}/control` | Controlar atuador (on/off) |
| `GET` | `/api/history/{sensor_id}` | Histórico de um sensor |
| `POST` | `/api/images` | Upload de imagem da webcam |

**Exemplo de request:**
```bash
curl -X POST http://localhost/api/sensors/1/data \
  -H "Authorization: Bearer YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"temperature": 23.5, "humidity": 65}'
```

## 📸 Screenshots

> *Em breve: capturas de ecrã do dashboard, gráficos e interface mobile*

## 🎯 Roadmap & Melhorias Futuras

- [ ] Notificações push quando valores ultrapassam limites
- [ ] Integração com Alexa/Google Home
- [ ] App móvel nativa (React Native)
- [ ] Machine Learning para previsão de tendências
- [ ] Suporte para múltiplas localizações
- [ ] Dashboard público (modo "kiosk")
- [ ] Exportação de relatórios em PDF
- [ ] Integração com serviços meteorológicos externos

## 🤝 Contribuir

Contribuições são bem-vindas! Se queres melhorar este projeto:

1. Faz fork do repositório
2. Cria um branch para a tua feature (`git checkout -b feature/MinhaFeature`)
3. Commit das alterações (`git commit -m 'Adiciona MinhaFeature'`)
4. Push para o branch (`git push origin feature/MinhaFeature`)
5. Abre um Pull Request

## 💬 Suporte

Se encontrares algum problema ou tiveres sugestões:
- 🐛 [Reportar bug](https://github.com/vitorianfonseca/uni-iot-weather-dashboard/issues)
- 💡 [Sugerir feature](https://github.com/vitorianfonseca/uni-iot-weather-dashboard/issues)

## 📝 Licença

Este projeto foi desenvolvido para fins educacionais no âmbito da UC de Tecnologias de Internet.

---

<div align="center">

**Feito com ☕ e 💻 por estudantes apaixonados por IoT**

⭐ Se gostaste do projeto, deixa uma estrela!

</div>
