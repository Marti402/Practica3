# Practica3
Participants: Alexandre Pascual / Marti Vila
```c++
#include <WiFi.h>
#include <WebServer.h>
#include <Arduino.h>

// Credenciales de la red WiFi
const char* ssid = "Nautilus"; 
const char* password = "20000Leguas"; 

// Creación del servidor en el puerto 80
WebServer server(80);

// Prototipo de la función handle_root
void handle_root();

// Página HTML que se mostrará en el navegador
String HTML = "<!DOCTYPE html>\
<html>\
<head>\
    <meta charset='UTF-8'>\
    <meta name='viewport' content='width=device-width, initial-scale=1.0'>\
    <title>ESP32 WebServer</title>\
    <style>\
        body { font-family: Arial, sans-serif; text-align: center; margin: 50px; }\
        h1 { color: #333; }\
    </style>\
</head>\
<body>\
    <h1>Mi Primera Página con ESP32 - Station Mode &#128522;</h1>\
</body>\
</html>";

// Función para manejar la raíz del servidor
void handle_root() {
    server.send(200, "text/html", HTML);
}

// Configuración inicial del ESP32
void setup() {
    Serial.begin(115200);
    Serial.println("Conectando a WiFi...");

    WiFi.begin(ssid, password);
    
    // Esperar conexión WiFi
    while (WiFi.status() != WL_CONNECTED) {
        delay(1000);
        Serial.print(".");
    }

    Serial.println("\nWiFi conectado con éxito.");
    Serial.print("Dirección IP: ");
    Serial.println(WiFi.localIP());  // Muestra la IP asignada

    // Configuración del servidor
    server.on("/", handle_root);
    server.begin();
    Serial.println("Servidor HTTP iniciado.");
}

// Bucle principal del ESP32
void loop() {
    server.handleClient();
}

```
