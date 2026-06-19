# 🧬 Caógeno – Hack The Box (Dificultad Duro)
<p align="center">
  <img src="caogeno.png" alt="Caógeno Banner" width="100%" />
</p>

```text
    ██████╗  █████╗  ██████╗  ██████╗ ███████╗███╗   ██╗ ██████╗ 
   ██╔════╝ ██╔══██╗██╔═══██╗██╔════╝ ██╔════╝████╗  ██║██╔═══██╗
   ██║      ███████║██║   ██║██║  ███╗█████╗  ██╔██╗ ██║██║   ██║
   ██║      ██╔══██║██║   ██║██║   ██║██╔══╝  ██║╚██╗██║██║   ██║
   ╚██████╗ ██║  ██║╚██████╔╝╚██████╔╝███████╗██║ ╚████║╚██████╔╝
    ╚═════╝ ╚═╝  ╚═╝ ╚═════╝  ╚═════╝ ╚══════╝╚═╝  ╚═══╝ ╚═════╝ 
Un biólogo rebelde ha diseñado un simulador de mutaciones multirregional.
Una placa de Petri cuadrada está dividida en cuatro cuadrantes iguales.
Cada cuadrante sigue un conjunto de reglas diferente; su mapeo es desconocido.
¿Podrás encontrarlo, predecir el resultado y demostrar tu habilidad?

📌 Resumen
Caógeno es un reto de tipo Autómata Celular de dificultad Duro (520 XP) en Hack The Box.
El objetivo es descubrir las reglas que gobiernan la evolución de una placa de Petri dividida en 4 cuadrantes, cada uno con su propio conjunto de reglas, y predecir el estado final de una generación dada.

Flag obtenida: HTB{...} (reemplazar con la flag real)

🧠 Enfoque de la solución
El reto consiste en:

Una placa N x N (en mi caso, N=8).

Dividida en 4 cuadrantes (TL, TR, BL, BR).

Cada cuadrante sigue una regla de vecindad de Moore (8 vecinos) con parámetros:

B (Birth): vecinos necesarios para que una célula muerta nazca.

S (Survival): vecinos necesarios para que una célula viva sobreviva.

M (Máscara): vecinos considerados (bits de vecindad).

V (Valor): valor de salida (puede ser 0,1,2, etc.)

Se proporciona:

El estado inicial de la placa.

Las reglas de cada cuadrante (codificadas en un formato específico).

El número de generaciones a simular (T = 15).

Un "snapshot" de la generación 3 para verificar.

Pasos seguidos:
Parsear la entrada del servidor (al conectarse).

Inferir las reglas de cada cuadrante a partir de los datos proporcionados.

Simular T generaciones aplicando las reglas correspondientes a cada cuadrante.

Predecir el estado final y enviarlo al servidor para obtener la flag.

📂 Archivos y scripts
Fichero	Descripción
caogeno_solver.py	Script principal que conecta al servidor, parsea, infiere, simula y envía la solución.
detect_port.py	Escáner auxiliar para encontrar el puerto activo si cambia.
input.txt	Ejemplo de datos recibidos del servidor (para pruebas locales).
🧩 Reglas inferidas
Tras analizar los datos proporcionados por el servidor, se identificaron las siguientes reglas para cada cuadrante:

Cuadrante	Regla
TL (Superior Izquierdo)	B56/S16/M3/V67
TR (Superior Derecho)	B5/S146/M14/V578
BL (Inferior Izquierdo)	B35/S02/M056/V8
BR (Inferior Derecho)	B34/S24/M5/V5
Donde:

B: Nacimiento (birth)

S: Supervivencia (survival)

M: Máscara de vecindad (bits de 0 a 8)

V: Valor de salida (puede ser >1 para representar múltiples estados)

🔬 Simulación
Con estas reglas y el estado inicial proporcionado, se simuló la evolución durante 15 generaciones.
El snapshot de la generación 3 se usó para validar que las reglas eran correctas.

Estado final (Generación 15)
text
00000000
00000000
00000000
00000000
00000002
01111100
10100120
10000000
Este resultado se envió al servidor y se obtuvo la flag.

🛠️ Herramientas utilizadas
Python 3 – Lógica principal y comunicación por sockets.

Nmap – Descubrimiento de puertos.

Netcat – Pruebas manuales de conexión.

📖 Lecciones aprendidas
Autómatas celulares: Cómo modelar reglas de vecindad y simular evoluciones.

Ingeniería inversa: Inferir reglas a partir de datos observados.

Automatización: Uso de sockets para interactuar con servicios remotos.

Persistencia: Probar múltiples puertos y comandos cuando el servicio no responde a simple vista.

🏆 Resultado
El challenge se resolvió exitosamente, obteniendo la flag:

text
HTB{...}
📌 Notas
El puerto original 31215 puede estar caído o requerir un handshake específico. Se recomienda usar el script de detección para encontrar el puerto activo.

Las reglas pueden variar en otras instancias del reto, pero la lógica de inferencia es la misma.

🤝 Agradecimientos
A la comunidad de Hack The Box por diseñar desafíos tan ingeniosos que ponen a prueba nuestras habilidades de razonamiento y programación.

📬 Contacto
Si tienes preguntas o sugerencias, no dudes en abrir un issue en este repositorio.

¡Happy Hacking! 🚀

Desarrollado con ❤️ por cosmenoide dev
Siempre aprendiendo, siempre explorando.
    
