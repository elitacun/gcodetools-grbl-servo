Esta es una versión modificada de la clásica extensión **Gcodetools** para Inkscape. Está diseñada específicamente para **Pen Plotters** y máquinas CNC DIY que utilizan un **servomotor** para subir y bajar el lápiz en lugar de un motor paso a paso en el eje Z.

---

## 🚀 Características Principales

* **Soporte Nativo para Servos:** Reemplaza los movimientos de `Z+` y `Z-` por comandos de potencia de husillo (`M3 Sxxx` y `M5`).
* **Interfaz de Usuario Integrada:** Añade 4 nuevos campos en la pestaña de opciones para configurar el hardware sin editar el código fuente.
* **Gestión de Delays (Retardos):**
    * **Servo Down Delay:** Asegura que el lápiz toque el papel antes de iniciar el movimiento en X/Y.
    * **Servo Up Delay:** Evita rayones accidentales al levantar el lápiz antes de un movimiento rápido.

---

## 🛠️ Instalación

1.  Descarga los archivos `gcodetools.py` y `gcodetools_pen_plotter.inx`.
2.  Copia ambos archivos en la carpeta de extensiones de Inkscape:
    * **Linux: (Appimage)** `~/.config/inkscape/extensions/`
    * **Windows:** `%APPDATA%\\inkscape\\extensions\\`
    * **macOS:** `~/Library/Application Support/org.inkscape.Inkscape/config/inkscape/extensions/`
3. Copiar el archivo footer al directorio output (tu carpeta de salida configurada donde se guardan los gcode generados por gcodetools)
4.  Reinicia Inkscape.

---

## ⚙️ Configuración en Inkscape

En el menú `Extensiones > Gcodetools > 1 Path to Gcode Pen Plotter`, navega a la pestaña **Preferences** para ver los nuevos parámetros:

| Parámetro | Valor Sugerido | Descripción |
| :--- | :--- | :--- |
| **Servo UP Command** | `M3 S125` | Comando para levantar el servo. |
| **Servo DOWN Command** | `M3 S0` | Comando para bajar el servo. |
| **Servo Delay Up** | `0.1` | Segundos de espera tras subir. |
| **Servo Delay Down** | `0.1` | Segundos de espera tras bajar. |

---

## 📖 Ejemplo de G-code Generado

La extensión limpia las coordenadas Z y añade los retardos automáticamente:

```gcode
(Inicio de trazo)
M3 S0         ; Baja el lápiz (Servo Down)
G4 P0.1       ; Delay para asegurar contacto
G1 X10 Y20 F500
...
(Fin de trazo)
M3 S125       ; Sube el lápiz (Servo Up)
G4 P0.1       ; Delay para asegurar retiro
G0 X50 Y50    ; Movimiento rápido de traslado
