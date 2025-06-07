# Practica-ESP32-con-DHT11-y-LCD
En este repositorio se mostrara como programar un ESP32 con un sensor DHT11, con el cual obtendremos las magnitudes de temperatura y humedad y se mostraran en una pantalla LCD.

## Introducción 

La placa ESP32 la empleamos para adquirir los datos provenientes del DHT11 (temperatura y humedad en porcentaje) respecto al entorno. 

La pantalla LCD se empleara para mostrar los datos solicitados:
- Nombre del diplomado
- Nombre
- Carrera profesional
- Fecha
- Temperatura
- Humedad

Esta practica se realizo empleando un simulador: [WOKWI](www.wokwi.com) la cual nos permite simular los elementos y el codigo.

# Material necesario

Para realizar esta practica se necesito
- [WOKWI](www.wokwi.com)
- Una tarjeta ESP32 (para adquisicion de datos)
- Sensor DHT11 (para recolectar los datos del entorno)
- LCD 16x2 (I2C)

# Instrucciones
1. Abrir la terminal del codigo:

Codigo empleado:

```
#include "DHTesp.h"
#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4

const int DHT_PIN = 15;

DHTesp dhtSensor;

LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

void setup() {

  Serial.begin(115200);
  dhtSensor.setup(DHT_PIN, DHTesp::DHT22);
  lcd.init();
  lcd.backlight();

}

void loop() {

  TempAndHumidity  data = dhtSensor.getTempAndHumidity();
  Serial.println("Temp: " + String(data.temperature, 1) + "°C");
  Serial.println("Humidity: " + String(data.humidity, 1) + "%");
  Serial.println("---");
  
  //Mostrar Diplomado (fila 1); mostrar Automatizacion (fila 2)
  lcd.setCursor(0, 0);
  lcd.print("   Diplomado    ");
  lcd.setCursor(0, 1);
  lcd.print(" Automatizacion ");
  delay(2000);
  lcd.clear();

  //Mostrar nombre (fila 1); mostrar carrera (fila 2)
  lcd.setCursor(0, 0);
  lcd.print(" Hector Vega R. ");
  lcd.setCursor(0, 1);
  lcd.print(" Ing. Mecanica  ");
  
  delay(2000);
  lcd.clear();

  //Mostrar fecha (fila 1)
  lcd.setCursor(0, 0);
  lcd.print("07 de Junio 2025");
  lcd.setCursor(0, 1);
  lcd.print(" ");
  delay(2000);
  lcd.clear();

  //Mostrar temperatura (fila 1); mostrar humedad (fila 2)
  lcd.setCursor(0, 0);
  lcd.print("  Temp: " + String(data.temperature, 1) + "\xDF"+"C  ");
  lcd.setCursor(0, 1);
  lcd.print("Humidity: " + String(data.humidity, 1) + "% ");
  delay(2000);
  lcd.clear();


}
```

2. Instalar la libreria de DHT senson library for ESPx y en la siguiente imagen se muestran las librerias empleadas.

![](https://github.com/HV202506/Practica-ESP32-con-DHT11-y-LCD/blob/main/LIBRERIAS.png?raw=true)

3. Hacer las concexiones del DHT11 y la pantalla LCD con el ESP32  tal cual se muestra la siguiente imagen.

![](https://github.com/HV202506/Practica-ESP32-con-DHT11-y-LCD/blob/main/conexion.png?raw=true)

## Librerias empleadas
1. DHT sensor library for ESPx
2. LiquidCrystal I2C

# Intrucciones de operación

1. Iniciar la simulación.
2. Observar los datos del monitor serial.
3. Colorar la temperatura y humedad dando doble click en el sensor DHT11 (temperatura y humedad).
4. Observar los datos mostrados en la pantalla LCD

# Resultados

Una vez realizados los pasos anteriores deberas visualizar los elementos solicitados en la pantalla LCD

## Pantalla 1:

![](https://github.com/HV202506/Practica-ESP32-con-DHT11-y-LCD/blob/main/Diplomado.png?raw=true)

## Pantalla 2:

![](https://github.com/user-attachments/assets/4e412b30-b40c-45be-a267-39b58cb14dea)

## Pantalla 3:

![image](https://github.com/user-attachments/assets/fddf7ac1-e135-4109-9730-7128a510173e)

## Pantalla 4:

![image](https://github.com/user-attachments/assets/c605a898-812f-4040-8882-b68b450a98da)


# Créditos

Desarrollado por: Ing. Héctor Angel Vega Rodríguez




