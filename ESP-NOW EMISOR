import network
import espnow
from machine import Pin

# Inicializa la interfaz WiFi en modo Station
sta = network.WLAN(network.STA_IF)
sta.active(True)

# Configura el LED en el Pin 2
led = Pin(2, Pin.OUT)
led.off()  # Asegura que el LED esté apagado al inicio

# Inicializa ESP-NOW
e = espnow.ESPNow()
e.active(True)

# Agrega la dirección MAC del transmisor (cambiar con la dirección real)
mac = b'\xa0\xa3\xb3)G\xf8'  # MAC del transmisor (Cambia por tu código MAC)
e.add_peer(mac)

# Bucle principal para recibir mensajes
while True:
    host, msg = e.recv()  # Espera hasta recibir un mensaje
    if msg == b'ON':
        led.on()  # Enciende el LED
        print("LED encendido")
    elif msg == b'OFF':
        led.off()  # Apaga el LED
        print("LED apagado")

