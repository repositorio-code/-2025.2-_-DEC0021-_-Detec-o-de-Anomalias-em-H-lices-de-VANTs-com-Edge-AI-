# -2025.2-_-DEC0021-_-Detec-o-de-Anomalias-em-H-lices-de-VANTs-com-Edge-AI-
# Detecção de Anomalias em Hélices de VANTs com Edge AI

> Projeto de Trabalho de Conclusão de Curso (TCC) - UFSC Campus Araranguá

Este repositório contém o código-fonte, esquemas e documentação do sistema embarcado desenvolvido para detectar falhas estruturais e operacionais (desbalanceamento) em sistemas rotativos de drones utilizando Inteligência Artificial na borda (*TinyML*).

**Autor:** [Nikolas Lopes]
**Orientador:** [Prof. Rodrigo Pereira, DR.]

---

## 📖 Introdução

A segurança operacional de Veículos Aéreos Não Tripulados (VANTs) depende criticamente da integridade de seus sistemas de propulsão. Falhas em hélices, como rachaduras ou desbalanceamentos, podem levar a vibrações excessivas e quedas catastróficas.

Este projeto propõe uma solução de baixo custo baseada em **Edge AI** (Inteligência Artificial na Borda). Utilizando um microcontrolador Arduino Nano 33 BLE Sense e a plataforma Edge Impulse, desenvolvemos um modelo capaz de classificar em tempo real, através da análise de vibração (FFT), os seguintes estados operacionais:
1. **Motor Parado**
2. **Motor Ligando** (Transitório)
3. **Motor Ligado** (Operação Normal)
4. **Anomalia** (Hélice Desbalanceada/Danificada)

A solução elimina a necessidade de telemetria para a nuvem, garantindo latência mínima e maior autonomia.

---

## 🛠 Hardware Necessário

Lista de materiais utilizados na construção da bancada de testes e do sistema embarcado:

| Componente | Modelo Específico | Função |
| :--- | :--- | :--- |
| **Microcontrolador** | Arduino Nano 33 BLE Sense | Processamento de IA e leitura do sensor IMU (LSM9DS1). |
| **Motor Brushless** | D2836 (Série 2217) - 1000KV | Propulsão principal do sistema de teste. |
| **ESC** | Controlador de 40A | Controle de velocidade do motor. |
| **Hélices** | Modelo 1045 (Plástico) | Uma íntegra e outra com fita adesiva para simular desbalanceamento. |
| **Fonte de Bancada** | Ajustável (12V) | Simulação de bateria LiPo 3S. |

---

## 🔌 Esquema de Conexão

A conexão física é simplificada devido aos sensores integrados do Nano 33 BLE Sense.

1. **Fixação do Sensor:** O Arduino deve ser fixado rigidamente à base do motor (usando fita dupla face forte e abraçadeiras) para garantir que o acelerômetro interno capture as vibrações mecânicas.
2. **Alimentação:** O Arduino é alimentado via cabo USB (durante o desenvolvimento/monitoramento serial).
3. **Controle do Motor:** O ESC é conectado ao motor (3 fios) e alimentado pela fonte 12V. O sinal de controle PWM do ESC pode ser gerado por um gerador de sinal externo ou por um pino PWM de outro microcontrolador auxiliar (para isolar o ruído elétrico, se necessário).

---

## 🚀 Instalação e Configuração

### 1. Ambiente de Software Necessário
Para reproduzir este projeto, você precisará das seguintes ferramentas instaladas:

*   [**Arduino IDE**](https://www.arduino.cc/en/software) (Versão 2.0 ou superior recomendada).
*   **Pacote de Placas Arduino Mbed OS:** No Arduino IDE, vá em *Boards Manager* e instale o suporte para "Arduino Mbed OS Nano Boards".
*   **Conta no Edge Impulse:** Para treinar ou retreinar o modelo.

### 2. Clonando o Repositório
git clone https://github.com/repositorio-code/-2025.2-_-DEC0021-_-Detec-o-de-Anomalias-em-H-lices-de-VANTs-com-Edge-AI-/


### 3. Importando a Biblioteca do Modelo
O modelo de IA treinado foi exportado como uma biblioteca Arduino.
1. Baixe o arquivo `.zip` da biblioteca (disponível na pasta `/library` deste repositório).
2. No Arduino IDE, vá em `Sketch > Include Library > Add .ZIP Library...` e selecione o arquivo.

---

## 💻 Projeto Final (Firmware)

O código principal (`main.ino`) está localizado na pasta `/src`. Ele realiza o seguinte fluxo:

1. **Inicialização:** Configura o acelerômetro IMU e carrega o modelo TensorFlow Lite for Microcontrollers.
2. **Loop Principal:**
    *   Lê os dados de aceleração (eixos X, Y, Z).
    *   Preenche o buffer de DSP (Digital Signal Processing).
    *   Executa a inferência da Rede Neural.
    *   Imprime no Serial Monitor a classe detectada e sua probabilidade (ex: `Anomalia: 0.98`).


---

## 📚 Tutoriais e Referências

Durante o desenvolvimento, alguns desafios foram superados. Abaixo, links úteis e soluções:

*   **Edge Impulse - Data Collection:** Utilizamos o *Data Forwarder* para enviar dados do Arduino direto para a plataforma via Serial. [Tutorial Oficial](https://docs.edgeimpulse.com/docs/tools/edge-impulse-cli/cli-data-forwarder).
*   **Problema de Ruído:** Inicialmente, fios soltos causavam leituras falsas. **Solução:** Uso de cabos blindados e fixação rígida do Arduino com abraçadeiras.
*   **Frequência de Amostragem:** Ajustada para 100Hz para respeitar o Teorema de Nyquist considerando a rotação máxima do motor nos testes.

---

## 📄 Licença

Este projeto é de código aberto e está licenciado sob a [MIT License](LICENSE).

