# Módulo bluetooth y potenciómetro con raspberry pi pico

# Tabla de contenidos
1. [Materiales](#Materiales)
2. [Descripción](#Descripción)
3. [Código](#Código)

## Materiales
* Raspberry pi pico
* Módulo bluetooth
* Protoboard
* Jumpers
* Potenciómetro


## Descripción

El módulo bluetoooth nos permite hacer proyectos de manera inalámbrica, también lo podemos conectar a otros dispositivos como: celulares, computadoras, microcontroladores, etc.

Se tienen dos tipos de módulos bluetooth, e  HC06 que funciona como esclavo, y el HC05 que funciona como esclavo y maestro.

Partes de un servomotor:
- Key: Para alternar entre el modo de datos.
- VCC: pin de alimentación del módulo, generalmente de 3.3 V a 6 V
-GND: pin de tierra del módulo.
-TX: pin de transmisión en serie de los datos.
-RX: pin de recepción en serie de los datos.

![bluetooth_frit](https://github.com/victorgjacobo/bluetooth_potenciometro_raspberry_pi_pico/assets/141197135/3a6aa30f-2e0f-4b8a-95ef-d18ad391cdfe)


Para la configuración del módulo bluetooth, se tienen que hacer mediante comandos AT, algunos de estos comandos se muestran en la siguiente tabla:

| Comando | Descripción | Respuesta |
|----------|----------|----------|
| AT+PSWD=XXXX    | Establecer una contraseña   |  ok   |
| AT+NAME= "Nombre"   | Cambiar el nombre del módulo  |  ok   | 
| AT+CMODE= "Mode"    | Cambiar el modo de conexión  |  ok   | 
| AT+ROLE= "Role"   | Cambiar el modo de trabajo, 0: esclavo, 1: maestro  |  ok   | 
| AT+BIND= "Address"   | Especificar la dirección del dispositivo al cual nos vamos a conectar  |  ok   | 
|  AT+VERSION?  | Obtener la versión del firmware  |  +VERSION   | 
|  AT+RESET   | Resetear el módulo  | ok   |


ElEn la figura de abajo se muestra la conexión del módulo bluetooth con la raspberry pi pico. Para capturar la señal del potenciómetro se hace uso del pin `pot -> GPIO 26`, para el puerto TX el pin `TX -> GPIO 4` y para el puerto RX el pint `RX -> GPIO 5`.

![segunda_practica](https://github.com/victorgjacobo/bluetooth_potenciometro_raspberry_pi_pico/assets/141197135/c8b638c6-6698-434c-aa44-d1f29e73852b)

## Código
```python
"""
  Nombre de la práctica: Potenciómetro con módulo Bluetooth
  Microcontrolador Raspberry Pi Pico
  Autor: Ing. Víctor González Jacobo
"""
##Declaración de las librerias
from machine import ADC,Pin, UART
from utime import sleep, sleep_ms

##Configuración del puerto UART
serial = UART(0, 9600)
### Declaración de los pines físicos
val_pot = ADC(26)

factor_16 = 3.3 / (65535)

def main():    
    print("Inicio del programa")
    while True:        
        voltaje = val_pot.read_u16() * factor_16
        buffer = "Voltaje: " + (str(voltaje))+'\n'
        serial.write(buffer)
        sleep(2)
    
if __name__ == '__main__':
    main()
```

![](https://img.shields.io/github/watchers/victorgjacobo/bluetooth_potenciometro_raspberry_pi_pico)
![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![Raspberry Pi](https://img.shields.io/badge/-RaspberryPi-C51A4A?style=for-the-badge&logo=Raspberry-Pi)
![GitHub followers](https://img.shields.io/github/followers/victorgjacobo)
