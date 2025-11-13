# 🧢Aplicação de Tecnologia Embarcada para Acessibilidade de Pessoas​ com Deficiência Visual

Este projeto usa um sensor ultrassônico para medir distância e aciona um buzzer quando algo se aproxima a menos de 30 cm. O código é estruturado com FreeRTOS, usando duas tarefas:

- **Tarefa 1:** Mede a distância com o sensor HC-SR04
- **Tarefa 2:** Aciona o buzzer conforme a distância

## 🛠 Métodos
 °Materiais Utilizados:​

 o Boné comum​

 o Arduino Uno​

 o Sensor ultrassônico HC-SR04​

 o Buzzer piezoelétrico​

 o Jumpers, protoboard e fonte de alimentação portátil​

°Procedimentos:​

 o Fixação do sensor ultrassônico na aba frontal do boné.​

 o Programação do Arduino para medir a distância entre    o sensor e obstáculos à frente.​

 o Configuração do buzzer para emitir um som quando a  distância for igual ou inferior a 30 cm.​

 o Testes em ambiente controlado com diferentes tipos  de obstáculos.​

 o Avaliação da resposta do sistema e conforto do usuário.

## 📦 Código
O código foi desenvolvido na IDE Arduino

```cpp
#include <Arduino_FreeRTOS.h>

const int trigPin = 9;
const int echoPin = 10;
const int buzzerPin = 8;

volatile int distance = 0;

void TaskUltrasonic(void *pvParameters);
void TaskBuzzer(void *pvParameters);

void setup() {
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  pinMode(buzzerPin, OUTPUT);
  Serial.begin(9600);

  xTaskCreate(TaskUltrasonic, "Ultrasonic", 128, NULL, 2, NULL);
  xTaskCreate(TaskBuzzer, "Buzzer", 128, NULL, 1, NULL);
}

void loop() {}


void TaskUltrasonic(void *pvParameters) {
  long duration;
  for (;;) {
    digitalWrite(trigPin, LOW);
    vTaskDelay(1);
    digitalWrite(trigPin, HIGH);
    vTaskDelay(1);
    digitalWrite(trigPin, LOW);

    duration = pulseIn(echoPin, HIGH);
    distance = duration * 0.034 / 2;

    Serial.print("Distancia: ");
    Serial.print(distance);
    Serial.println(" cm");

    vTaskDelay(100);
  }
}


void TaskBuzzer(void *pvParameters) {
  for (;;) {
    if (distance <= 30) {
      digitalWrite(buzzerPin, HIGH);
    } else {
      digitalWrite(buzzerPin, LOW);
    }
    vTaskDelay(50);
  }
}

```
## 📟Guia de Montagem

![Guia de Montagem](git.png)


