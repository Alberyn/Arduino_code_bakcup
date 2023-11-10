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
