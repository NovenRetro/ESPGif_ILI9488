ESPGif 🎞️ (ESP32 + ILI9488 + SD/SPIFFS) — by NovenRetro

ESPGif (ILI9488 edition) es un firmware para ESP32 que reproduce GIFs animados e imágenes JPG/JPEG en pantallas ILI9488 de gran formato (480×320), permitiendo administrar el contenido desde una interfaz web alojada en el propio ESP32 (subir, listar, reproducir y borrar archivos).

Este proyecto es una variante específica de ESPGif, optimizada y adaptada para pantallas grandes ILI9488, manteniendo compatibilidad con microSD y SPIFFS, e incorporando autocentrado y re-escalado automático para imágenes estáticas.

📌 Nota importante
Este repositorio está pensado exclusivamente para ILI9488.
Para pantallas ST7735 (128×160) existe un repositorio separado.

🆚 Diferencias clave vs versión ST7735
Característica	ST7735	ILI9488
Resolución	128×160	480×320
Tamaño de pantalla	1.8"	3.5" / 4"
Controlador	ST7735	ILI9488
Profundidad de color	RGB565	RGB565 (convertido desde RGB888)
Rendimiento GIF	Fluido	Limitado por resolución
JPG/JPEG	Sí	Sí (recomendado)
Uso recomendado	GIFs animados	JPG + GIFs simples

👉 En ILI9488 no se busca fluidez extrema en GIFs grandes, sino calidad visual, tamaño, y compatibilidad con imágenes estáticas.

✅ Features
🎞️ Multimedia

Reproducción de GIFs animados

Reproducción de imágenes JPG / JPEG

Autocentrado automático (GIF y JPG)

Re-escalado automático de JPG:

Mantiene relación de aspecto

Reduce imágenes grandes a 480×320

Centra imágenes más pequeñas sin estirarlas

Conversión correcta de color RGB888 → RGB565

Render compatible con pantallas ILI9488 vía SPI

💾 Almacenamiento

microSD (altamente recomendado)

Fallback automático a SPIFFS

Estructura simple basada en /gifs/

🌐 Interfaz Web (mobile-friendly)

Subir GIF o JPG

Listar archivos almacenados

Reproducir cualquier media

Eliminar archivos

Indicador de “Reproduciendo ahora”

⚙️ Sistema

mDNS → acceso por http://espgif.local

Improv Wi-Fi Serial

Compatible con ESP Web Tools

Configuración Wi-Fi sin recompilar firmware

🧩 Hardware soportado

ESP32 DevKit / ESP32-WROOM

Pantalla ILI9488 SPI 480×320

Lector microSD (integrado o externo)

⚠️ IMPORTANTE
En pantallas ILI9488 SPI, el bus es un cuello de botella real.
Este firmware prioriza estabilidad y compatibilidad, no FPS altos.

🔌 Conexiones (pinout sugerido)
SPI (compartido)

SCLK → GPIO 18

MOSI → GPIO 23

MISO → GPIO 19 (solo SD)

TFT ILI9488

TFT_CS → GPIO 5

TFT_DC → GPIO 16

TFT_RST → GPIO 17

VCC → 3.3V (verificar módulo)

GND → GND

microSD

SD_CS → GPIO 4

VCC → 3.3V

GND → GND

📌 Pines definidos en el código:

#define SD_CS    4
#define SD_MOSI  23
#define SD_MISO  19
#define SD_SCLK  18

#define TFT_CS   5
#define TFT_DC   16
#define TFT_RST  17
#define TFT_SCLK 18
#define TFT_MOSI 23

📁 Estructura de archivos

Todos los archivos se almacenan en:

/gifs/


Archivos soportados:

.gif

.jpg

.jpeg

Archivo especial:

/gifs/idle.gif


Se reproduce automáticamente como idle al iniciar el sistema o cuando no hay contenido activo.

🌐 Interfaz Web
Home

Acceso por:

http://espgif.local

o por la IP local mostrada en pantalla

Permite:

Subir GIF o JPG

Ver lista de archivos

Reproducir cualquier media

Eliminar archivos

Ver qué archivo está en reproducción

💡 En pantallas ILI9488 se recomienda usar JPG como idle o imágenes principales.

🔧 Endpoints HTTP (API)
UI

GET /

GET /status

GET /list

Reproducción

POST /play?name=<archivo.gif|jpg>

POST /idle

POST /delete?name=<archivo>

POST /upload → subida multipart

Wi-Fi

POST /wifi/reset

🧠 Persistencia (NVS / Preferences)

Namespace: ESPGif

Wi-Fi

wifi_ssid

wifi_pass

🎨 Consideraciones de color (ILI9488)

La pantalla trabaja internamente en RGB565

JPGs se decodifican en RGB888 y se convierten correctamente

Si los colores se ven incorrectos:

Revisar orden RGB/BGR del módulo

Verificar librería y configuración del driver ILI9488

🧯 Troubleshooting

“GIFs grandes van lentos”

Es esperado en ILI9488 por SPI

Usar GIFs simples o JPG

“JPG se ve mejor que GIF”

Correcto y recomendado

El firmware está pensado para eso en pantallas grandes

“Se cuelga con SD”

Cambiar microSD

Formatear FAT32

Evitar SDs grandes o de baja calidad

📌 Créditos / Librerías

AnimatedGIF

JPEGDEC

Adafruit_GFX

Driver ILI9488

ESP32 Arduino Core

Improv Wi-Fi / ESP Web Tools

🤝 Contribuir

¡Las contribuciones son bienvenidas!

Fork del proyecto

Rama: feature/tu-mejora

Pull Request con descripción clara

📄 Licencia

MIT License
© NovenRetro 2025 — Todos los derechos reservados