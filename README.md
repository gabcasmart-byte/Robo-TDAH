# Robo-TDAH
Sistema de robótica assistiva que combina **visão computacional e inteligência artificial** para monitorar sinais relacionados à atenção durante atividades de estudo e fornecer intervenções adaptativas.
## O que o projeto faz?

O robô utiliza uma câmera para analisar o rosto do usuário em tempo real. A partir dos landmarks faciais, o sistema extrai características relacionadas à atenção e calcula o **Índice Computacional de Nível de Foco (ICNF)**.

A arquitetura utiliza dois modelos principais:

- **Cérebro 1 — XGBoost:** classificação do nível de atenção.
- **Cérebro 2 — MobileNetV2 + TFLite:** reconhecimento de expressões faciais.

Com base nas informações obtidas, o sistema pode gerar intervenções para auxiliar o usuário, como:

- **Animações para motivação**
- **Alertas**
- **Nenhuma ação**

## Como utilizar o código desse repositório?
### 1. Extrair a pasta na raspberry pi
### 2. Instalar dependências (só na primeira vez)
No terminal, digite:
```bash
pip install opencv-python mediapipe onnxruntime numpy
```
E pressione <kbd>Enter</kbd> para instalar
### 3. Rodar o sistema
### 3.1. Crie e abra codigo1.service para rodar o programa ao inicar o sistema
```bash
sudo nano /etc/systemd/system/codigo1.service
```
### 3.2. Digite isso no arquivo que abrir
**Lembre-se de substituir `/home/Downloads/Robo-TDAH/main.py` pelo caminho para o arquivo principal**
```bash
[Unit]
Description=Script de Inicializacao
After=network.target

[Service]
ExecStart=python3 /home/Downloads/Robo-TDAH/main.py
WorkingDirectory=/home/pi/
StandardOutput=inherit
StandardError=inherit
Restart=always
User=pi

[Install]
WantedBy=multi-user.target
```
Salve com <kbd>Ctrl+O</kbd>, depois <kbd>Enter</kbd>, e saia com <kbd>Ctrl + X</kbd>

### 3.3. Recarregue o daemon do systemd para reconhecer o novo serviço e ative-o:
```bash
sudo systemctl daemon-reload
```
E:
```bash
sudo systemctl enable codigo1.service
```
### 3.4. Inicie o serviço imediatamente para testar:
```bash
sudo systemctl start codigo1.service
```
## Uso responsável
* O sistema utiliza **câmera e análise facial**. Testes com pessoas devem respeitar consentimento, privacidade e as regras aplicáveis ao ambiente de pesquisa.

* O projeto é uma ferramenta complementar de suporte e **não tem como objetivo substituir psicólogos, psiquiatras ou outros profissionais especializados**.

## Autores

- Gabriel Castro Martins
- Heitor Sousa Farias de Lucena

- Orientador: Prof. Isaac Wanderson de Pontes Xavier
- Coorientadora: Lilian Daniele Duarte de Sousa

Colégio Paraíso — Juazeiro do Norte, Ceará — 2026
