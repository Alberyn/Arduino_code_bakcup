# practiseardino
**Включение по значениям светочувствительного механизма**

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



**Светофор**

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


**Зажигание кнопкой без запоминания**

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
