# Notas desarrollo electrónica:

Base funcionamiento C++ /2 servos

#include <Servo.h>

Servo servomotor1;
Servo servomotor2;

int aumentar1 = 3;  // Pin para el primer pulsador de aumentar la velocidad del primer servo
int disminuir1 = 5; // Pin para el segundo pulsador de disminuir la velocidad del primer servo
int aumentar2 = 6;  // Pin para el primer pulsador de aumentar la velocidad del segundo servo
int disminuir2 = 7; // Pin para el segundo pulsador de disminuir la velocidad del segundo servo

int velocidad1 = 90; // Velocidad inicial del primer servo (90 es parar)
int velocidad2 = 90; // Velocidad inicial del segundo servo (90 es parar)

void setup() {
  servomotor1.attach(9);  // Pin PWM 9 del Arduino para el primer servo
  servomotor2.attach(10); // Pin PWM 10 del Arduino para el segundo servo

  pinMode(disminuir1, INPUT_PULLUP); // Configurar pulsadores del primer servo con resistencia pull-up
  pinMode(aumentar1, INPUT_PULLUP);
  pinMode(disminuir2, INPUT_PULLUP); // Configurar pulsadores del segundo servo con resistencia pull-up
  pinMode(aumentar2, INPUT_PULLUP);

  servomotor1.write(velocidad1);  // Inicialmente parar el primer servo
  servomotor2.write(velocidad2);  // Inicialmente parar el segundo servo
}

void loop() {
  // Leer el estado de los pulsadores del primer servo
  int buttonStateAumentar1 = digitalRead(aumentar1);
  int buttonStateDisminuir1 = digitalRead(disminuir1);

  // Control del primer servomotor
  if (buttonStateAumentar1 == LOW) {
    servomotor1.write(0); // 0 es una dirección
  } else if (buttonStateDisminuir1 == LOW) {
    servomotor1.write(180); // 180 es la dirección opuesta
  } else {
    servomotor1.write(88); // Ajustar según sea necesario para detener el primer servo
  }

  // Leer el estado de los pulsadores del segundo servo
  int buttonStateAumentar2 = digitalRead(aumentar2);
  int buttonStateDisminuir2 = digitalRead(disminuir2);

  // Control del segundo servomotor
  if (buttonStateAumentar2 == LOW) {
    servomotor2.write(0); // 0 es una dirección
  } else if (buttonStateDisminuir2 == LOW) {
    servomotor2.write(180); // 180 es la dirección opuesta
  } else {
    servomotor2.write(89); // Ajustar según sea necesario para detener el segundo servo
  }

  delay(0); // Ajustar el delay según sea necesario para la respuesta de los servos
}
