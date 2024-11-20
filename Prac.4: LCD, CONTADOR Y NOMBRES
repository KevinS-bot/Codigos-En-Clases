import network
import espnow
from machine import Pin, I2C
from i2c_lcd import I2cLcd  # Importa la biblioteca I2C_LCD
import time

# Inicializa la interfaz Wi-Fi en modo Estación
sta = network.WLAN(network.STA_IF)
sta.active(True)

# Configura I2C para la pantalla LCD (asumiendo SCL en GPIO22 y SDA en GPIO21)
i2c = I2C(scl=Pin(22), sda=Pin(21))

# Inicializa la pantalla LCD 16x2 (la dirección I2C es usualmente 0x27 o 0x3F)
lcd_display = I2cLcd(i2c, 0x27, 2, 16)  # 0x27 es una dirección I2C común para LCD 16x2

# Inicializa ESP-NOW
e = espnow.ESPNow()
e.active(True)

# Agrega la dirección MAC del transmisor (cámbiala a la dirección MAC real)
mac = b'\xa0\xa3\xb3)G\xf8'  # Dirección MAC de ejemplo del transmisor
e.add_peer(mac)

# Muestra un mensaje inicial en la pantalla LCD
lcd_display.clear()
lcd_display.putstr("Esperando mensaje...")

# Bucle principal para recibir mensajes
while True:
    host, msg = e.recv()  # Espera hasta recibir un mensaje
    
    if msg == b'ON':
        # Bucle que ejecuta la secuencia continuamente
        
            # Muestra el primer nombre
            lcd_display.clear()
            lcd_display.putstr("Kevin Suqui")  # Muestra el primer nombre
            print("Mensaje recibido: Nombre 1: Kevin")
            time.sleep(2)  # Espera 2 segundos

            # Muestra el contador del 1 al 10
            lcd_display.clear()
            for i in range(1, 11):
                lcd_display.putstr(f"Contando: {i}")  # Muestra el contador
                print(f"Contando: {i}")
                time.sleep(1)  # Espera 1 segundo
                lcd_display.clear()  # Limpia la pantalla entre cada número

            # Muestra el segundo nombre
            lcd_display.clear()
            lcd_display.putstr("Juan Siavichay")  # Muestra el segundo nombre
            print("Mensaje recibido: Nombre 2: Juan")
            time.sleep(2)  # Espera 2 segundos

            # Al terminar, espera a que el pulsador sea presionado de nuevo para empezar la secuencia
            lcd_display.clear()
            lcd_display.putstr("Esperando mensaje...")
            time.sleep(2)  # Mensaje de espera antes de recibir el siguiente mensaje

    elif msg == b'OFF':
        # Resetear la pantalla a estado predeterminado
        lcd_display.clear()
        lcd_display.putstr("Esperando mensaje...")  # Mensaje predeterminado
        print("Esperando mensaje...")

    # Añade un pequeño retraso para evitar que la CPU se sobrecargue
    time.sleep(0.1)
