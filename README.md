# 🛏️ Sistema de Deteção de Queda na Cama
### Desenvolvido por João Pereira Nº7 & Nuno Pereira Nº12
**Escola Secundária Latino Coelho | Curso: Técnico de Eletrónica, Automação e Computadores | 2025/2026**

---

## 📋 Descrição

Sistema de deteção de queda baseado em dois sensores ultrassónicos HC-SR04,
controlados por um Arduino Uno. Quando um objeto (ou pessoa) é detetado a
≤ 15 cm do sensor, o sistema ativa um LED vermelho e um buzzer de alerta.
Em estado normal, o LED verde permanece ligado.

---

## 📐 Posicionamento dos Sensores

A instalação correta dos sensores é **essencial** para o bom funcionamento do sistema.

### 📍 SENSOR DA ESQUERDA
- Colocar do **lado esquerdo** da cama, olhando de frente para ela
- Posicionar a **≈ 7 cm do chão**
- O sensor deve ficar **paralelo ao chão**, apontado para baixo da cama
- Distância de deteção configurada: **≤ 15 cm**

### 📍 SENSOR DA DIREITA
- Colocar do **lado direito** da cama, olhando de frente para ela
- Posicionar a **≈ 7 cm do chão**
- O sensor deve ficar **paralelo ao chão**, apontado para baixo da cama
- Distância de deteção configurada: **≤ 15 cm**

> ⚠️ **ATENÇÃO:** Não apontar os sensores um para o outro.
> Devem estar paralelos entre si e perpendiculares ao chão.
> Evitar superfícies muito inclinadas ou reflexivas perto dos sensores,
> pois podem causar leituras erradas.

---

## 🔌 Ligações dos Componentes

### SENSOR DA ESQUERDA
| Componente      | Pino Arduino |
|-----------------|-------------|
| HC-SR04 TRIGGER | D9          |
| HC-SR04 ECHO    | D10         |
| LED Verde       | D2          |
| LED Vermelho    | D4          |
| Buzzer          | D5          |

### SENSOR DA DIREITA
| Componente      | Pino Arduino |
|-----------------|-------------|
| HC-SR04 TRIGGER | D13         |
| HC-SR04 ECHO    | D3          |
| LED Verde       | D7          |
| LED Vermelho    | D11         |
| Buzzer          | D6          |

> 💡 Não esquecer de ligar resistências de **220 Ω** em série com cada LED
> para proteger os componentes.

---

## ⚙️ Como Funciona o Código

### 1. Inicialização (`setup`)
- Configura todos os pinos como INPUT ou OUTPUT
- Liga os LEDs verdes de ambos os sensores
- Imprime informação de arranque no Monitor Serial

### 2. Loop Principal (`loop`)
O loop repete-se continuamente a cada **200 ms** e segue esta ordem: 
[1] Lê o SENSOR DA ESQUERDA
│
├─ Distância ≤ 15 cm? ──► LED VERMELHO ON + BUZZER ON
│
└─ Distância > 15 cm? ──► LED VERDE ON (estado normal)
[pausa 50 ms para evitar interferência entre sensores]
[2] Lê o SENSOR DA DIREITA
│
├─ Distância ≤ 15 cm? ──► LED VERMELHO ON + BUZZER ON
│
└─ Distância > 15 cm? ──► LED VERDE ON (estado normal)
[pausa 200 ms]
[repete]

### 3. Cálculo da Distância
O sensor emite um pulso ultrassónico de **10 µs** pelo pino TRIGGER.
O pino ECHO mede o tempo que o som demora a regressar.
A distância é calculada pela fórmula:  Distância (cm) = Duração (µs) × 0,034 ÷ 2

Se não houver resposta em **30 ms**, o sensor considera leitura inválida
e mantém o LED verde ligado por segurança.

### 4. Monitor Serial
Abre o Monitor Serial a **9600 baud** para ver as leituras em tempo real:


=== Sistema de Deteção de Queda — 2 Sensores ===
[ SENSOR DA ESQUERDA ] Distancia: 42 cm  |  Estado: Normal (sem deteção)
[ SENSOR DA DIREITA  ] Distancia: 11 cm  |  Estado: *** QUEDA DETETADA ***



---

## 🔍 Estados do Sistema

| Estado           | LED Verde | LED Vermelho | Buzzer | Serial                  |
|------------------|-----------|--------------|--------|-------------------------|
| Normal (>15 cm)  | ✅ ON     | ❌ OFF       | ❌ OFF | Normal (sem deteção)    |
| Queda (≤15 cm)   | ❌ OFF    | ✅ ON        | ✅ ON  | *** QUEDA DETETADA ***  |
| Sem leitura      | ✅ ON     | ❌ OFF       | ❌ OFF | Sem leitura válida      |

> 🔒 Em caso de erro de leitura, o sistema mantém o LED verde ligado
> por segurança, evitando falsos alarmes.

---

## ⚠️ Dicas de Instalação

- Fixar os sensores com suporte firme para não vibrarem
- Manter os sensores afastados de superfícies metálicas
- Testar as leituras no Monitor Serial antes de colocar em funcionamento
- O `delay(50ms)` entre os dois sensores é obrigatório para evitar
  que os ultrassons de um sensor interfiram com o eco do outro

---

*PAP 2025/2026 — Escola Secundária Latino Coelho*
