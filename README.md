# practise ardino

**Включение по значениям светочувствительного механизма**
```c++
void setup() {
  Serial.begin(9600);
  pinMode(7, OUTPUT);
  pinMode(A3, INPUT);
  pinMode(A0, INPUT);
}

void loop() {

  
  int photo = analogRead(A0);
  int ptr = analogRead(A3);

  if (photo > svich) {
    digitalWrite(7, HIGH);

  }
  else {
    digitalWrite(7, LOW);
  }

  //digitalWrite(7, HIGH);
  //delay(1000);
  //digitalWrite(7, LOW);
  //delay(2000);

  Serial.println("Photo: " + String(photo) + ", Ptr: " + String(ptr) );

}

```

**Светофор**
```c++
//Coded by Jevins Annson of J4 Jevins
//Subscribe To J4 Jevins Youtube :- https://www.youtube.com/J4Jevins

const int FirstLed = 5;
const int SecondLed = 6;
const int ThirdLed = 7;
int counter;
  
void setup() {
  
  pinMode (FirstLed, OUTPUT);
  pinMode (SecondLed, OUTPUT);
  pinMode (ThirdLed, OUTPUT);
}

void loop() {

  
    for (counter = 0; counter < 2; ++counter) {

        digitalWrite (FirstLed, HIGH);
        delay (1000);
        digitalWrite (SecondLed, HIGH);
        delay (500);
        digitalWrite (FirstLed, LOW);
        delay (1000);
        digitalWrite (ThirdLed, HIGH);
        delay (500);
        digitalWrite (SecondLed, LOW);
        delay(1000);
        digitalWrite (SecondLed, HIGH);
        delay (500);
        digitalWrite (ThirdLed, LOW);
        delay (1000);
        digitalWrite (SecondLed, LOW);
        

    }
}
```

**Зажигание кнопкой без запоминания**

```c++
#define FirstLed 5
#define SecondLed  6
#define ThirdLed  7
#define dot  8
  
  
void setup() {
  
  pinMode (FirstLed, OUTPUT);
  pinMode (SecondLed, OUTPUT);
  pinMode (ThirdLed, OUTPUT);
  pinMode (dot, INPUT);
}

void loop() {
int btnVal = digitalRead(dot);

if (btnVal == 0)
{

    digitalWrite(FirstLed, HIGH);
    digitalWrite(SecondLed, HIGH);
    digitalWrite(ThirdLed, HIGH);
 
  }
  else {

    digitalWrite(FirstLed, LOW);
    digitalWrite(SecondLed, LOW);
    digitalWrite(ThirdLed, LOW);
  }

}
```

**Зажигание светодиодов с сохранение результата нажатия**


```c++
#define FirstLed 5
#define SecondLed  6
#define ThirdLed  7
#define dot  8

bool btnState = false;
 //сохраняется результат нажатия кнопки - диоды вкл без постоянного нажатия кнопки и наоборот 
void setup() {
  
  pinMode (FirstLed, OUTPUT);
  pinMode (SecondLed, OUTPUT);
  pinMode (ThirdLed, OUTPUT);
  pinMode (dot, INPUT);
}

void loop() {

int btnVal = digitalRead(dot);

if (btnVal == 0){

  btnState = !btnState;
}

if (btnState)
{

    digitalWrite(FirstLed, HIGH);
    digitalWrite(SecondLed, HIGH);
    digitalWrite(ThirdLed, HIGH);
 
  }
  else {

    digitalWrite(FirstLed, LOW);
    digitalWrite(SecondLed, LOW);
    digitalWrite(ThirdLed, LOW);
  }

}
```


**RGB подстветка**

[Библиотека для подсветки](https://github.com/wilmouths/RGBLed)

```c++
#include <RGBLed.h>

#define RED_PIN 9
#define GREEN_PIN 11
#define BLUE_PIN 10

RGBLed led(RED_PIN, GREEN_PIN, BLUE_PIN, RGBLed::COMMON_ANODE);

void setup() {
pinMode(RED_PIN, OUTPUT);
  pinMode(GREEN_PIN, OUTPUT);
  pinMode(BLUE_PIN, OUTPUT);
}

void loop() {
//led.setColor(RGBLed::YELLOW);
//led.setColor(200, 120, 0);
led.brightness(20); // 50% brightness
//led.fadeOut(210, 150, 0, 3, 1000);

led.crossFade(RGBLed::RED, RGBLed::GREEN, 5, 1000);  // Fade from RED to GREEN in 5 steps during 100ms 
}
```

**Термометр**

[Сайт для примеров с Амперкой](http://wiki.amperka.ru/%D0%BF%D1%80%D0%BE%D0%B4%D1%83%D0%BA%D1%82%D1%8B:troyka-temperature-sensor)
```c++
    // библиотека для работы с аналоговым термометром (Troyka-модуль)
    #include <TroykaThermometer.h>
     
    // создаём объект для работы с аналоговым термометром
    // и передаём ему номер пина выходного сигнала
    TroykaThermometer thermometer(A0);
     
    void setup()
    {
      // открываем последовательный порт
      Serial.begin(9600);
    }
     
    void loop()
    {
      // считываем данные с аналогового термометра
      thermometer.read();
      // вывод показателей аналогового термометра в градусах Цельсия
      Serial.print("Temperature is ");
      Serial.print(thermometer.getTemperatureC());
      Serial.println(" C");
      // вывод показателей аналогового термометра в градусах Кельвина
      Serial.print("Temperature is ");
      Serial.print(thermometer.getTemperatureK());
      Serial.println(" K");
      // вывод показателей аналогового термометра в градусах Фаренгейта
      Serial.print("Temperature is ");
      Serial.print(thermometer.getTemperatureF());
      Serial.println(" F");
      delay(1000);
    }
```

**Вывод значения температуры на дисплей**

[Дисплей амперки](http://wiki.amperka.ru/%D0%BF%D1%80%D0%BE%D0%B4%D1%83%D0%BA%D1%82%D1%8B:troyka:quad-display-v2)

```c++
// Подключаем библиотеку для работы с дисплеем
#include <QuadDisplay2.h>
#include <TroykaThermometer.h>
// создаём объект класса QuadDisplay и передаём номер пина CS
QuadDisplay qd(9);
TroykaThermometer thermometer(A0);
 
void setup()
{
  qd.begin();
  Serial.begin(9600);
}

void loop() {
  thermometer.read();
// можно показывать температуру в °C
  qd.displayTemperatureC(thermometer.getTemperatureC());
  delay(1000);
 
  qd.displayClear();
  qd.displayTemperatureC(thermometer.getTemperatureF());
  delay(1000);
  qd.displayClear();
  qd.displayTemperatureC(thermometer.getTemperatureK());
  delay(1000);
}

```


**Вращения сервопривода от амперки**

```c++

    #include <AmperkaServo.h>
     
    // Создаём объект для работы с сервомоторами
    AmperkaServo servo;
     
    // Задаём имя пина, к которому подключён сервопривод
    constexpr uint8_t SERVO_PIN = 9;
     
    void setup() {
      // Подключаем сервомотор
      // servo.attach(SERVO_PIN);
      // Подключаем сервомотор с расширенными параметрами
      // Советуем использовать именно этот вариант для точной настройки мотора  
      // servo.attach(pin, minPulseWidth, maxPulseWidth, minAngle, maxAngle);
      // - pin: номер пина, к которому подключён сервопривод
      // - minPulseWidth: ширина импульса, соответствующая минимальному углу поворота. 
      // Опциональный и по умолчанию стоит 544 мкс.
      // - maxPulseWidth: ширина импульса, соответствующая максимальному углу поворота. 
      // Опциональный и по умолчанию стоит 2400 мкс.
      // - minAngle: минимальный угол поворота сервопривода. 
      // Опциональный и по умолчанию стоит 0°.
      // - maxAngle: максимальный угол поворота сервопривода. 
      // Опциональный и по умолчанию стоит 180°.
      // Данные возьмите из технических характеристик мотора
      servo.attach(SERVO_PIN, 544, 2400, 0, 180);
    }
     
    void loop() {
      // Устанавливаем минимальный угол
      servo.writeAngle(servo.getMinAngle());
      // Ждём 1 секунду
      delay(1000);
      // Устанавливаем среднее положение
      servo.writeAngle(servo.getMidAngle());
      // Ждём 1 секунду
      delay(1000);
      // Устанавливаем максимальный угол
      servo.writeAngle(servo.getMaxAngle());
      // Ждём 1 секунду
      delay(1000);
      // Устанавливаем среднее положение
      servo.writeAngle(servo.getMidAngle());
      // Ждём 1 секунду
      delay(1000);
    }
```

**Изменение угла сервопривода с помощью потенциометра**

[Servo](https://docs.arduino.cc/learn/electronics/servo-motors)

```c++
#include <Servo.h>
#define potpin A0

Servo myservo;  // create servo object to control a servo


int val;    // variable to read the value from the analog pin

void setup() {
  myservo.attach(9);  // attaches the servo on pin 9 to the servo object
  pinMode(potpin, INPUT);
}

void loop() {
  val = analogRead(potpin);            // reads the value of the potentiometer (value between 0 and 1023)
  val = map(val, 0, 1023, 0, 180);     // scale it to use it with the servo (value between 0 and 180)
  myservo.write(val);                  // sets the servo position according to the scaled value
  delay(15);                           // waits for the servo to get there
}
```

**Кручение двух моторов в одну и в другую сторону**

[Моторы](http://wiki.amperka.ru/%D0%BF%D1%80%D0%BE%D0%B4%D1%83%D0%BA%D1%82%D1%8B:arduino-motor-shield)

```c++
/ подключите один мотор к клемме: M1+ и M1-
// а второй к клемме: M2+ и M2-
// Motor shield использует четыре контакта 4, 5, 6, 7 для управления моторами 
// 4 и 7 — для направления, 5 и 6 — для скорости
#define SPEED_1      5 
#define DIR_1        4
 
#define SPEED_2      6
#define DIR_2        7
 
void setup() {
  // настраиваем выводы платы 4, 5, 6, 7 на вывод сигналов 
  for (int i = 4; i < 8; i++) {     
    pinMode(i, OUTPUT);
  }
} 
 
void loop() {
  // устанавливаем направление мотора «M1» в одну сторону
  digitalWrite(DIR_1, LOW);
  // включаем мотор на максимальной скорости
  analogWrite(SPEED_1, 255);
  // ждём одну секунду
  delay(1000);
 
  // устанавливаем направление мотора «M1» в другую сторону
  digitalWrite(DIR_1, HIGH);
  // ждём одну секунду
  delay(1000);
  // выключаем первый мотор
  analogWrite(SPEED_1, 0);
 
  // устанавливаем направление мотора «M2» в одну сторону
  digitalWrite(DIR_2, LOW);
  // включаем второй мотор на максимальной скорости
  analogWrite(SPEED_2, 255);
  // ждём одну секунду
  delay(1000);
 
  // устанавливаем направление мотора «M2» в другую сторону
  digitalWrite(DIR_2, HIGH);
  // ждём одну секунду
  delay(1000);
 
  // выключаем второй мотор
  analogWrite(SPEED_2, 0);
  // ждём одну секунду
  delay(1000);
}
```

**Управление моторами при помощи пульта (инфокрасное излучение)**

```c++
#include <IRremote.hpp>

#define IR_RECEIVE_PIN 11
#define IR_BUTTON_PLUS 21
#define IR_BUTTON_MINUS 7
#define IR_BUTTON_1 12
#define IR_BUTTON_2 24
#define IR_BUTTON_3 94

#define SPEED_1      5 
#define DIR_1        4
 
#define SPEED_2      6
#define DIR_2        7

void setup(){
  Serial.begin(9600);
  IrReceiver.begin(IR_RECEIVE_PIN);

  for (int i = 4; i < 8; i++) {     
    pinMode(i, OUTPUT);
  }
}

void loop(){
   if (IrReceiver.decode()) {
      IrReceiver.resume(); // Enable receiving of the next value
      int command = IrReceiver.decodedIRData.command;
      
      switch (command) {
        case IR_BUTTON_PLUS: {
          digitalWrite(DIR_1, LOW); // set direction
          analogWrite(SPEED_1, 255); // set speed

          digitalWrite(DIR_2, LOW); // set direction
          analogWrite(SPEED_2, 255); // set speed

          break;
        }
        case IR_BUTTON_MINUS: {
          digitalWrite(DIR_1, HIGH); // set direction
          analogWrite(SPEED_1, 255); // set speed

          digitalWrite(DIR_2, HIGH); // set direction
          analogWrite(SPEED_2, 255); // set speed

          break;
        }
        case IR_BUTTON_1: { // stop mototrs
          digitalWrite(DIR_1, HIGH); // set direction
          analogWrite(SPEED_1, 255); // set speed

          digitalWrite(DIR_2, LOW); // set direction
          analogWrite(SPEED_2, 255); // set speed

          break;
        }
        case IR_BUTTON_2: { 
          digitalWrite(DIR_1, LOW); // set direction
          analogWrite(SPEED_1, 255); // set speed

          digitalWrite(DIR_2, HIGH); // set direction
          analogWrite(SPEED_2, 255); // set speed
          
          break;
        }
        case IR_BUTTON_3: { // stop mototrs
          analogWrite(SPEED_1, 0); 
          analogWrite(SPEED_2, 0);  
          break;
        }
      }
  }
}
```

**Управление мотором через джойстик**

```c++
#define SPEED_1      5 
#define DIR_1        4
 
#define SPEED_2      6
#define DIR_2        7

#define ux A0


void setup(){
  Serial.begin(9600);
  pinMode (ux, INPUT);
  
  for (int i = 4; i < 8; i++) {     
    pinMode(i, OUTPUT);
  }
}

void loop(){
  Serial.println(analogRead(ux));
  delay(200);
  int command = analogRead(ux);

  if (command < 200) {
       
    digitalWrite(DIR_1, LOW); // set direction
   analogWrite(SPEED_1, 255); // set speed
  }
  else if (command > 200 && command < 600){
  digitalWrite(DIR_1, HIGH); // set direction
   analogWrite(SPEED_1, 255);

  }
    else if (command > 600){
  digitalWrite(DIR_1, HIGH); // set direction
   analogWrite(SPEED_1, 0);

  }      

}
```
**Квадрат рисует**

```c++
#include <IRremote.hpp>

#define IR_RECEIVE_PIN 0
#define IR_BUTTON_PLUS 21
#define IR_BUTTON_MINUS 7
#define IR_BUTTON_CH_PLUS 71
#define IR_BUTTON_CH_MINUS 69
#define IR_BUTTON_PLAY_PAUSE 67

#define SPEED_1      5 
#define DIR_1        4
 
#define SPEED_2      6
#define DIR_2        7

void setup(){
  Serial.begin(9600);
  IrReceiver.begin(IR_RECEIVE_PIN);

  for (int i = 4; i < 8; i++) {     
    pinMode(i, OUTPUT);
  }
}

void loop(){
   if (IrReceiver.decode()) {
      IrReceiver.resume(); // Enable receiving of the next value
      int command = IrReceiver.decodedIRData.command;
      
      if (command = IR_BUTTON_MINUS) {
        
        
        
          digitalWrite(DIR_1, HIGH); // set direction
          analogWrite(SPEED_1, 255); // set speed

          digitalWrite(DIR_2, HIGH); // set direction
          analogWrite(SPEED_2, 255); // set speed

          delay(2000);

          digitalWrite(DIR_1, LOW); // set direction
          analogWrite(SPEED_1, 255); // set speed

          digitalWrite(DIR_2, HIGH); // set direction
          analogWrite(SPEED_2, 255); // set speed

          delay(5000);

          digitalWrite(DIR_1, HIGH); // set direction
          analogWrite(SPEED_1, 255); // set speed

          digitalWrite(DIR_2, HIGH); // set direction
          analogWrite(SPEED_2, 255); // set speed

          delay(2000);

          digitalWrite(DIR_1, LOW); // set direction
          analogWrite(SPEED_1, 255); // set speed

          digitalWrite(DIR_2, HIGH); // set direction
          analogWrite(SPEED_2, 255); // set speed

          delay(5000);

          digitalWrite(DIR_1, HIGH); // set direction
          analogWrite(SPEED_1, 255); // set speed

          digitalWrite(DIR_2, HIGH); // set direction
          analogWrite(SPEED_2, 255); // set speed

          delay(2000);

          digitalWrite(DIR_1, LOW); // set direction
          analogWrite(SPEED_1, 255); // set speed

          digitalWrite(DIR_2, HIGH); // set direction
          analogWrite(SPEED_2, 255); // set speed

          delay(5000);

          digitalWrite(DIR_1, HIGH); // set direction
          analogWrite(SPEED_1, 255); // set speed

          digitalWrite(DIR_2, HIGH); // set direction
          analogWrite(SPEED_2, 255); // set speed

          delay(2000);

          analogWrite(SPEED_1, 0); 
          analogWrite(SPEED_2, 0);  



          
      }
  }
}
```

