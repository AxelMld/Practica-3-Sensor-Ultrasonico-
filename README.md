# PRACTICA 3 Sensor ultrasonico de distancia con ESP32

## Para esta practica se utilizo 

* Modulo ESP32
* sensor Ultrasonico de distancia 
* LCD de 3 Pines

## Para la simulacion nos dirigimos a la pagina  

woki : https://wokwi.com

#### Dashboard de pagina a utilizar 

## Pasos a Seguir 

1. Seleccionar el modulo ESP32 
2. Escoger los dispositivos a utilizar 
3. Realizar las conexiones como se muestra en el apartado "conexion"
4. Bajar las librerias mencionadas en el apartado "librerias" 



## Conexion 

![]()

## Librerias 

2. LiquidCrystal I2C

## Codigo utilizado 


```

#include "DHTesp.h"
#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4

const int Trigger = 13;   //Pin digital 2 para el Trigger del sensor
const int Echo = 12;   //Pin digital 3 para el Echo del sensor

LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);


void setup() {
  
  Serial.begin(9600);//iniciailzamos la comunicación
  pinMode(Trigger, OUTPUT); //pin como salida
  pinMode(Echo, INPUT);  //pin como entrada
  digitalWrite(Trigger, LOW);//Inicializamos el pin con 0

  lcd.init();
  lcd.backlight();
}

void loop()
{

  long t; //timepo que demora en llegar el eco
  long d; //distancia en centimetros


  digitalWrite(Trigger, HIGH);
  delayMicroseconds(10);          //Enviamos un pulso de 10us
  digitalWrite(Trigger, LOW);
  
  t = pulseIn(Echo, HIGH); //obtenemos el ancho del pulso
  d = t/59;             //escalamos el tiempo a una distancia en cm
  
  Serial.print("Distancia: ");
  Serial.print(d);      //Enviamos serialmente el valor de la distancia
  Serial.print("cm");
  Serial.println();
  delay(1000);          //Hacemos una pausa de 100ms


   lcd.setCursor(0, 0);
  lcd.print("Distancia: " + String(d) + "cm");
  lcd.setCursor(0, 1);
  lcd.print("Axel M");
  delay(2000);


}


```


# Resultados
![]()



# Creditos 

Axel Miranda.

