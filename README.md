# HEAMON

HEAMON es un prototipo experimental para explorar señales visuales asociadas al rendimiento humano mediante monitorización continua. El monitor permanece activo mientras se realizan ventanas independientes de análisis de **30 segundos**; al terminar cada ventana genera un resumen heurístico y lo compara con el análisis completado anterior en la misma pestaña.

**No es una herramienta de diagnóstico médico ni determina si alguien está apto para una tarea.** El índice y sus categorías no tienen validación clínica y no deben utilizarse para decisiones de salud, seguridad o misión. Una ventana de 30 segundos es una medida exploratoria y puede no ser suficiente para estimar con estabilidad algunas variables, especialmente la respiración.

## Funcionamiento

1. Ejecuta la aplicación y pulsa **Iniciar monitor**. Autoriza el acceso a la cámara; la monitorización continúa hasta pulsar **Detener monitor**.
2. El panel en vivo actualiza los indicadores y sus unidades. El conteo global de parpadeos y el conteo del análisis son independientes.
3. Pulsa **Iniciar análisis (30 s)** para abrir una ventana de medición. Al terminar, se presenta el resultado sin apagar la cámara ni el monitor.
4. Inicia otro análisis cuando quieras. El nuevo informe compara sus valores con los de la ventana completada inmediatamente antes.

La comparación se mantiene solo en memoria mientras la pestaña siga abierta. Al recargar o cerrar la pestaña se borra el historial. El vídeo no se graba ni se envía a un servidor.

## Métricas y unidades

- Conteo de pestañeadas: total desde el inicio del monitor y conteo independiente por análisis.
- Frecuencia de pestañeo: `pestañeadas/min`; monitor con ventana móvil de 60 s y análisis calculado sobre su ventana de 30 s.
- PERCLOS: porcentaje (`%`) de tiempo con ojos estimados cerrados sobre tiempo con rostro válido.
- Duración media de cierre ocular: milisegundos (`ms`) por cierre detectado.
- EAR: relación de aspecto ocular, adimensional.
- Respiración: respiraciones por minuto (`resp/min`), estimación experimental de periodicidad de brillo en una ROI aproximada del torso.
- Inclinación roll: grados (`°`), proxy 2D calculado a partir de landmarks oculares.
- Movimiento de cabeza: desviación normalizada, adimensional; proxy de variación de landmarks, no pose clínica.
- RGB periocular: canales RGB de 0 a 255; informativo y excluido del índice.
- Cobertura facial: proporción de tiempo con detección facial válida; no es una medida de confianza.

## Índice experimental

El resumen puede combinar PERCLOS (30 %), duración de cierre (25 %), frecuencia de parpadeo (20 %), respiración (15 %) y movimiento de cabeza (10 %). Los componentes no disponibles se excluyen y los pesos restantes se normalizan. Sin datos suficientes, el índice no se calcula. Pesos y umbrales son heurísticas de demostración, no valores validados ni probabilidad de fatiga.

El RGB periocular no puntúa. La estimación respiratoria por vídeo no equivale a una medición fisiológica validada. Los cambios de iluminación, encuadre, movimiento, ropa, postura, lentes y diferencias individuales pueden alterar las señales. Además, una sesión más corta ofrece menos muestras y puede aumentar la incertidumbre; los resultados de 30 s deben interpretarse con esa limitación.

## Ejecutar localmente

La cámara requiere un contexto seguro (`localhost` o HTTPS). Desde la raíz del repositorio ejecuta:

```bash
python -m http.server 8000
```

Abre <http://localhost:8000>. Se necesita conexión a internet para descargar MediaPipe y su modelo desde CDN.

## Privacidad y límites

El vídeo se procesa en el navegador; el prototipo no almacena ni transmite vídeo. La cámara debe permanecer activa para que continúe el monitor. Si se detiene el flujo de cámara, la monitorización se detiene también.

HEAMON no sustituye evaluación profesional, protocolos de misión ni validación con datos de referencia. El uso formal requeriría protocolo controlado, evaluación de errores, revisión ética y validación apropiada.
