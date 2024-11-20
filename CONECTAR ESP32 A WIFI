# FUNCION PARA ESTABLECER CONEXION WIFI

def do_connect(SSID, PASSWORD):
    import network
    global sta_if
    sta_if = network.WLAN(network.STA_IF)
    if not sta_if.isconnected():
        sta_if.active(True)
        sta_if.connect(SSID, PASSWORD)
        print('Conectado a la red', SSID + "...")
        while not sta_if.isconnected():
            pass
        print('Configuracion de red (IP/netmask/gw/DNS):', sta_if.ifconfig())

do_connect('clases1', '12345678')
