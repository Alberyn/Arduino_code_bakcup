# practiseardino
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

https://github.com/wilmouths/RGBLed

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
