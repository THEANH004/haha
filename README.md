#include <LiquidCrystal_I2C.h>

void speedControl() {
    left_motor_speed = initial_motor_speed - PID_value;
    right_motor_speed = initial_motor_speed + PID_value;

    left_motor_speed = constrain(left_motor_speed, 0, 255);
    right_motor_speed = constrain(right_motor_speed, 0, 255);

    analogWrite(ENA, left_motor_speed);
    analogWrite(ENB, right_motor_speed);
}

void motorControl() {
    if (error > 0) {
        robotTurnLeft();
    } else if (error < 0) {
        robotTurnRight();
    } else {
        robotForward();
    }
}

void robotForward() {
    digitalWrite(in[0], HIGH);
    digitalWrite(in[1], LOW);
    digitalWrite(in[2], HIGH);
    digitalWrite(in[3], LOW);
}

void robotStop() {
    for (int i = 0; i < 4; i++) {
        digitalWrite(in[i], LOW);
    }
}

void robotTurnLeft() {
    digitalWrite(in[0], LOW);
    digitalWrite(in[1], HIGH);
    digitalWrite(in[2], HIGH);
    digitalWrite(in[3], LOW);
}

void robotTurnRight() {
    digitalWrite(in[0], HIGH);
    digitalWrite(in[1], LOW);
    digitalWrite(in[2], LOW);
    digitalWrite(in[3], HIGH);
}
