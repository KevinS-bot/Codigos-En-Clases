import network
import espnow
from machine import Pin, I2C
from i2c_lcd import I2cLcd  # Import the I2C_LCD library
import time

# Initialize the Wi-Fi interface in Station mode
sta = network.WLAN(network.STA_IF)
sta.active(True)

# Set up I2C for the LCD screen (assuming SCL on GPIO22 and SDA on GPIO21)
i2c = I2C(scl=Pin(22), sda=Pin(21))

# Initialize the 16x2 LCD screen (I2C address is usually 0x27 or 0x3F)
lcd_display = I2cLcd(i2c, 0x27, 2, 16)  # 0x27 is a common I2C address for 16x2 LCDs

# Initialize ESP-NOW
e = espnow.ESPNow()
e.active(True)

# Add the MAC address of the transmitter (change to the actual MAC address)
mac = b'\xa0\xa3\xb3)G\xf8'  # Example MAC address
e.add_peer(mac)

# Display an initial message on the LCD
lcd_display.clear()
lcd_display.putstr("Waiting for msg...")

# Function to display a message letter by letter
def display_message_letter_by_letter(message):
    lcd_display.clear()
    for char in message:
        lcd_display.putstr(char)  # Display one character
        time.sleep(0.2)  # Wait for 0.2 seconds before showing the next character

# Main loop to receive messages
while True:
    host, msg = e.recv()  # Wait until a message is received
    if msg == b'ON':
        display_message_letter_by_letter("HOLA MUNDO")  # Display "HOLA MUNDO" letter by letter
        print("Message received: HOLA MUNDO")
    elif msg == b'OFF':
        lcd_display.clear()
        lcd_display.putstr("Waiting for msg...")  # Default message
        print("Waiting for message...")
    
    # Add a short delay to avoid the CPU getting overloaded
    time.sleep(0.1)
