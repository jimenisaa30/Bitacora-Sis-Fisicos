# Bitácora de Desarrollo - Unidad 2: Visuales Generativas y Parametrizables
 

---

## 1. Intención y Concepto
Este proyecto explora la creación de un sistema visual generativo en tiempo real basado en patrones geométricos y simetrías dinámicas. La propuesta busca pasar de la generación de una imagen estática al diseño de **relaciones paramétricas**, donde el tiempo y las funciones matemáticas determinan la evolución de la forma y el color.

> *"La unidad de diseño ya no es la imagen, sino la relación que produce la imagen."*

---

## 2. Definición del Sistema (Input - Process - Output)

El sistema opera bajo la arquitectura procedural **Input-Process-Output**:

###  Entradas (Inputs / Parámetros)
* **Tiempo (`absTime.seconds`):** Actúa como el reloj global del sistema, haciendo modular la fase de la rampa de color y la animación de los patrones en tiempo real.
* **Frecuencia y Amplitud (CHOPs):** Valores numéricos que controlan la densidad y la velocidad de deformación del sistema.

###  Procesamiento (Process)
1. **Generación de Forma (CHOPs):** Se generan tres señales mediante nodos `Pattern` (seno, coseno y rampa) agrupados con nodos `Math` y `Merge` para crear una trayectoria helicoidal/espiral.
2. **Instanciación (SOPs/COMPs):** Se duplica la geometría sobre la posición de los puntos calculados.
3. **Composición y Deformación (TOPs):** Se aplican simetrías con nodos `Mirror` y repeticiones infinitas con `Tile`, seguidas de un mapa de desplazamiento (`Displace`) para generar el efecto fluido.
4. **Modulación Cromática:** Se utiliza un nodo `Ramp TOP` cuya fase oscila con el tiempo, conectado a un nodo `Lookup TOP` para remapear los tonos en escala de grises hacia una paleta de color personalizada.

###  Salida (Output)
* Sistema visual generativo interactivo renderizado a 60 FPS en tiempo real.

---

## 3. Diagrama de Nodos y Estructura

A continuación se muestra la red de nodos desarrollada en TouchDesigner:

![Diagrama de Nodos de TouchDesigner](<img width="1919" height="1031" alt="Captura de pantalla 2026-08-11 003452" src="https://github.com/user-attachments/assets/4868d566-0ed2-4b78-8da0-2fad1cc926ec" />
)
*Figura 1: Estructura general del sistema en TouchDesigner.*

---

## 4. Evolución Visual y Pruebas

### Fase 1: Estructura en Blanco y Negro (Base Procedural)
En la primera etapa se construyó la matriz de movimiento y las transformaciones de espejo sin información de color.

![Prueba Base Blanco y Negro](<img width="1910" height="1032" alt="Captura de pantalla 2026-08-10 201712" src="https://github.com/user-attachments/assets/fef98863-8cc3-481a-b620-c6196df2ce20" />)
*Figura 2: Generación del patrón base.*

### Fase 2: Aplicación de Paleta Cromática y Oscilación
Se integró la rampa de color animada para convertir la estructura geométrica en una experiencia visual dinámica.

![Resultado Final con Color](<img width="603" height="342" alt="Captura de pantalla 2026-08-10 234809" src="https://github.com/user-attachments/assets/b25c441e-4d70-4582-91c7-90d358294bb7" />)
*Figura 3: Resultado final con modulación de color activada.*

---

## 5. Demostración en Vivo (Video / GIF)

A continuación se muestra el comportamiento dinámico del sistema en ejecución:

![Demostración en Video](
https://github.com/user-attachments/assets/b4088821-7938-4fa0-8cfa-c632414310a3
)

---

## 6. Conclusiones y Decisiones de Diseño
* La utilización de nodos `CHOP` para coordinar posiciones matemáticas permitió una estructura fluida y ligera para el cómputo en GPU.
