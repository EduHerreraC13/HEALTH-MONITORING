# HEAMON

HEAMON es un prototipo experimental para evaluar señales humanas relevantes para la preparación operativa durante una sesión de 60 segundos. El objetivo no es diagnosticar enfermedades ni sustituir la valoración clínica o operacional; es explorar si una combinación de señales visuales puede servir como indicador preliminar de degradación del rendimiento humano.

## Enfoque de la solución

HEAMON combina variables compatibles con investigación previa sobre fatiga, somnolencia y deterioro operativo:

- PERCLOS: porcentaje del tiempo con ojos cerrados durante la ventana observada.
- Duración media de cierre ocular (AECD): tiempo medio de cada cierre detectado.
- Frecuencia de parpadeo: tasa estimada por minuto.
- Respiración estimada: variación óptica del torso y periodicidad detectada.
- Inclinación y estabilidad de la cabeza: proxy de posture 2D para identificar cabeceo o inestabilidad.
- Calidad de captura: tiempo en la cámara con detección facial válida.

La aplicación no utiliza el color periocular para puntuar. El RGB periocular solo se muestra como información contextual, porque la variación de iluminación, cámara y constitución individual hace que no sea un marcador fiable de fatiga por sí solo.

## Qué muestra la interfaz

- Tiempo restante de la sesión.
- Número de pestañeadas y frecuencia estimada por minuto.
- PERCLOS.
- Duración media de cierre ocular.
- Respiración experimental estimada.
- Posible roll/inclinación de la cabeza y estabilidad.
- Gráfico de evolución temporal de EAR y variación visual del torso.
- Informe final con índice heurístico, banda de estado, factores observados y recomendación prudente.

## Escala operativa (heurística)

El sistema es un índice experimental, no clínico. La banda se diseñó como referencia de estado operativo y debe entenderse como un indicador de señales observadas, no como diagnóstico médico o certeza de fatiga.

- 85–100: Óptimo
- 70–84: Bueno
- 50–69: Vigilancia
- 25–49: Riesgo
- 0–24: Crítico

## Cómo ejecutar

La cámara requiere HTTPS o localhost. Desde la raíz del repositorio:

```bash
python -m http.server 8000
```

Abre <http://localhost:8000>, concede el permiso de cámara y pulsa "Iniciar análisis (60 s)".

Es necesaria conexión a internet para cargar MediaPipe y el modelo del detector desde CDN.

## Estructura del análisis

Durante la sesión de 60 segundos, el sistema:

1. Detecta el rostro con MediaPipe.
2. Calcula EAR y cierre ocular para evaluar PERCLOS y duración media de cierre.
3. Anota pestañeadas y su tasa por minuto.
4. Extrae una ventana del torso para estimar respiración por variación óptica.
5. Calcula inclinación y estabilidad de la cabeza como proxy 2D.
6. Acumula señales para producir un índice final y un resumen de factores.

## Límites importantes

- HEAMON no diagnostica fatiga, estrés, somnolencia ni ninguna enfermedad.
- El sistema es un prototipo de investigación y no sustituye la supervisión humana ni la validación clínico-operacional.
- El ruido de cámara, movimiento, luz, lentes, postura o la propia variabilidad individual puede distorsionar la estimación.
- La respiración estimada es una señal óptica aproximada y no una medición fisiológica validada.
- El color periocular se muestra, pero no se usa para puntuar.

## Privacidad

El vídeo se procesa localmente en el navegador. Esta demo no almacena ni envía vídeos a un backend.

## Uso recomendado

HEAMON debe entenderse como una herramienta de apoyo para estudios preliminares, validación experimental y evaluación de señales humanas en entorno controlado. Para uso formal, con decisiones relevantes de salud, seguridad o operación, se requiere un protocolo validado, referencia clínica y supervisión profesional.
