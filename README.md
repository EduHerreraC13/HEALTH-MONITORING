# HEAMON

HEAMON es un prototipo experimental para explorar señales visuales asociadas al rendimiento humano en sesiones de monitorización continua. La cámara puede permanecer activa mientras se realizan ventanas independientes de análisis de 60 segundos. Al completar cada ventana se genera un resumen heurístico y se compara con el análisis completado anterior en la misma pestaña.

**No es una herramienta de diagnóstico médico ni determina si alguien está apto para una tarea.** El índice y sus categorías son experimentales, no tienen validación clínica y no deben usarse para decisiones de salud, seguridad o misión.

## Funcionamiento

1. Inicia el monitor; concede el permiso de cámara. La monitorización continúa hasta pulsar **Detener monitor**.
2. El panel en vivo actualiza los indicadores y sus unidades. El conteo global de parpadeos y el conteo del análisis de 60 segundos son independientes.
3. Pulsa **Iniciar análisis (60 s)** para abrir una ventana de medición. Al terminar, HEAMON muestra un resumen sin apagar la cámara ni el monitor.
4. Inicia otro análisis cuando quieras. El informe compara sus valores con la ventana anterior.

La comparación anterior se mantiene solo en memoria mientras la página siga abierta; al recargar o cerrar la pestaña se borra. El vídeo no se graba ni se envía a un servidor.

## Métricas y unidades

- Conteo de pestañeadas: número de cierres detectados; separado entre total del monitor y ventana de análisis.
- Frecuencia de pestañeo: pestañeadas por minuto (`pestañeadas/min`); en el panel continuo es una ventana móvil aproximada de 60 s.
- PERCLOS: porcentaje (`%`) de tiempo con ojos estimados cerrados sobre tiempo con rostro válido.
- Duración media de cierre ocular (AECD): milisegundos (`ms`) por cierre detectado.
- EAR: relación de aspecto ocular, adimensional.
- Respiración: respiraciones por minuto (`respiraciones/min`), estimación experimental a partir de periodicidad de brillo en una región aproximada del torso.
- Inclinación roll: grados (`°`), proxy 2D calculado a partir de los ojos.
- Movimiento de cabeza: desviación normalizada, adimensional; proxy de variación de landmarks, no pose clínica.
- RGB periocular: canales RGB de 0 a 255; solo informativo y excluido del índice.
- Cobertura facial: porcentaje de tiempo con detección facial válida; no es una medida de confianza.

## Índice experimental

El resumen puede combinar PERCLOS (30 %), duración de cierre (25 %), frecuencia de parpadeo (20 %), respiración (15 %) y movimiento de cabeza (10 %). Los componentes no disponibles se excluyen y los pesos restantes se normalizan. Sin datos suficientes, el índice no se calcula. Los pesos y umbrales son heurísticas de demostración, no valores validados ni probabilidad de fatiga.

El RGB periocular no puntúa: depende mucho de la iluminación, exposición, cámara y características individuales. La frecuencia respiratoria extraída de vídeo tampoco equivale a una medición fisiológica validada. Los perfiles del informe describen señales observadas, no diagnostican fatiga o estrés.

## Ejecutar localmente

La cámara requiere un contexto seguro (`localhost` o HTTPS). En la raíz del repositorio ejecuta:

```bash
python -m http.server 8000
```

Abre <http://localhost:8000>. Se requiere conexión a internet para cargar MediaPipe y su modelo desde CDN.

## Privacidad y límites

El procesamiento de vídeo se realiza en el navegador; el prototipo no almacena ni transmite vídeo. La cámara debe mantenerse activa para que continúe el monitor. Si se detiene el flujo de cámara, se detiene también la monitorización.

Los cambios de iluminación, encuadre, movimiento, ropa, postura, lentes y diferencias individuales pueden alterar las señales. HEAMON no sustituye evaluación profesional, protocolos de misión ni validación con datos de referencia. El uso formal requeriría un protocolo controlado, evaluación de errores, revisión ética y validación apropiada.
