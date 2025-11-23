# 💻 Firmware e Edge AI

Este diretório contém o código-fonte do sistema embarcado e a biblioteca de Inteligência Artificial gerada pela plataforma Edge Impulse.

## Estrutura do Código
O projeto foi desenvolvido para ser autossuficiente, rodando inteiramente no microcontrolador **Arduino Nano 33 BLE Sense** sem dependência de conexão constante com computadores ou nuvem.

### 1. `src/main.ino`
Este é o código principal (`sketch`) que deve ser carregado na placa. Suas funções são:
*   **Inicialização:** Configura o sensor IMU (LSM9DS1) e aloca memória para o modelo TFLite Micro.
*   **Coleta de Dados (In-loop):** Lê os valores de aceleração (X, Y, Z) a 100Hz.
*   **Inferência (In-loop):** Envia os dados brutos para a biblioteca do Edge Impulse.

### 2. `library/edge-impulse-sdk.zip`
Esta é a biblioteca C++ exportada do Edge Impulse. Ela contém:
*   **DSP (Digital Signal Processing):** O código otimizado para calcular a FFT (Transformada Rápida de Fourier) e o Filtro Passa-Alta diretamente no Arduino.
*   **Modelo Neural:** Os pesos e a arquitetura da Rede Neural Densa treinada.
*   **Motor de Inferência:** O runtime do TensorFlow Lite for Microcontrollers.
