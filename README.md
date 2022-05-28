# Sistema com Placa Solar Automatizado #


## Descrição ##

O projeto consiste em uma placa solar inteligente que define o seu grau de inclinação de acordo com a posição do sol, isso feito basicamente com dois sensores LDR e um servo motor. 

A inspiração do projeto veio das palestras da siemens sobre energia, realizadas em nosso auditório na fatec. Nela, os profissionais citam a busca por um desenvolvimento tecnológico mais sustentável. 

Os objetivos a serem alcançados consistem na experiência de saber como seria um mundo mais sustentável partindo de nós mesmos, fazendo uma breve demonstração de como isso pode se aplicar à dimensões maiores para aumentar o impacto na sustenstabilidae do mundo moderno. 



## Lista de materiais ##

+ Servo motor 
+ Sensores LDR
+ Jumpers 
+ Protoboard 
+ Arduino UNO
+ Suporte feito de madeira
+ Display LCD com I2C
+ Placa fotovoltaica 
+ LED
+ Resistores 
+ 



## Montagem ##
![WhatsApp Image 2022-05-28 at 14 10 49](https://user-images.githubusercontent.com/105353466/170837528-afe91d19-af78-40e8-ba09-f47f432bfbde.jpeg)



## Código fonte ##

``` #include <Servo.h> //including the library of servo motor
#include <Wire.h>
#include <LiquidCrystal_I2C.h>
Servo myservo;
LiquidCrystal_I2C lcd(0x27,16,2);
int initial_position = 90;
int LDR1 = A0; //connect The LDR1 on Pin A0
int LDR2 = A1; //Connect The LDR2 on pin A1
int error = 5;
int servopin=9; //You can change servo just makesure its on arduino's PWM pin
int inicio = millis();
void setup()
{
myservo.attach(servopin);
pinMode(LDR1, INPUT);
pinMode(LDR2, INPUT);
myservo.write(initial_position); //Move servo at 90 degree
delay(10);
lcd.init();
}
void loop()
{
int R1 = analogRead(LDR1); // read LDR 1
int R2 = analogRead(LDR2); // read LDR 2
int diff1= abs(R1 - R2);
int diff2= abs(R2 - R1);
if((diff1 <= error) || (diff2 <= error)) {
} else {
if(R1 > R2)
{
initial_position = --initial_position;
}
if(R1 < R2)
{
initial_position = ++initial_position;
}
}
myservo.write(initial_position);
delay(100);
if (millis()-inicio>1000){
lcd.clear();
lcd.setBacklight(HIGH);
lcd.setCursor(0,0);
lcd.print("LD1:");
lcd.setCursor(4,0);
lcd.print(R1);
lcd.setCursor(8,0);
lcd.print("LD2:");
lcd.setCursor(12,0);
lcd.print(R2);
lcd.setCursor(0,1);
lcd.print(" Projeto Solar");
delay (100);
inicio = millis();



}
} ```




## Resultados ##

Os resultados obtidos foram satisfatórios com o funcionamento mecânico do sistema, cumprindo o seu papel de ajustar a angulação das placas fotovoltaicas de acordo com a intensidade de luz de cada LDR, tendo os seus valores mostrados no display LCD. 
Apesar da baixa produção de energia pela placa, conseguimos atingir o objetivo de ligar o LED. Porém, esperávamos um pouco a mais de produtividade dessa placa.
Dentre as etapas, a mais trabalhosa foi a soldagem de componentes, por conta da pouca experiência que tivemos com esse processo. 
