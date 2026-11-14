# HEAMON — evaluación experimental de señales humanas

HEAMON es un prototipo web de investigación para explorar señales visuales durante una captura de 60 segundos. No es un dispositivo médico, no diagnostica fatiga o estrés y no determina aptitud para tareas operacionales.

## Qué presenta

- Conteo de pestañeadas y frecuencia aproximada por minuto.
- PERCLOS: porcentaje del tiempo con ojos estimados como cerrados, sobre el tiempo en que el rostro se detectó correctamente.
- Duración media de los cierres oculares detectados (AECD) y EAR medio.
- Estimación exploratoria de frecuencia respiratoria mediante periodicidad de cambios de brillo en una región aproximada del torso.
- Inclinación roll y variabilidad de posición de la cabeza como proxies 2D, no como pose clínica.
- Valor RGB periocular informativo, excluido del índice.
- Gráfico de la evolución de EAR y de la señal óptica del torso.
- Resumen de sesión con un índice heurístico multivariable, cobertura y factores observados.

## Índice experimental y límites de interpretación

El resumen combina, cuando están disponibles, PERCLOS (30 %), duración de cierre (25 %), frecuencia de parpadeo (20 %), respiración (15 %) y movimiento de cabeza (10 %). Los umbrales son heurísticas de demostración, no referencias clínicas ni puntos de corte validados. Si falta una señal, el índice renormaliza los pesos disponibles y muestra cuántos componentes se usaron; si no hay datos suficientes, no calcula el índice. La cobertura describe datos observados, no es un porcentaje de confianza.

El perfil “ocular”, “activación/movimiento” o “combinado” solo describe patrones heurísticos de señales. No diagnostica fatiga, estrés, ansiedad, somnolencia ni ninguna condición. El color bajo los ojos no se utiliza para puntuación porque cambia con iluminación, exposición, cámara y características individuales, y no permite inferir fatiga de forma fiable.

## Ejecutar localmente

La cámara requiere un contexto seguro (`localhost` o HTTPS). Desde la raíz del repositorio:

```bash
python -m http.server 8000
```

Abre <http://localhost:8000>, concede permiso de cámara y pulsa **Iniciar análisis (60 s)**. Se requiere conexión a internet para descargar MediaPipe y el modelo desde CDN. También puede servirse desde un hosting estático con HTTPS.

## Encuadre

Coloca el rostro centrado y deja visible el torso/pecho en la parte inferior del cuadro. La región verde indica la zona periocular; la azul es una ROI torácica aproximada. Mantén cámara, postura e iluminación lo más estables posible. Si el rostro no se detecta, la cobertura cae; si la respiración no tiene periodicidad óptica suficiente, se excluye del índice.

## Privacidad y validación

El vídeo se analiza en el navegador; esta demo no lo graba ni lo envía a un servidor. La descarga de MediaPipe/modelo requiere internet. El procesamiento de vídeo puede variar según dispositivo y navegador.

Las estimaciones pueden confundirse con parpadeo normal, sequedad ocular, postura, movimiento de cámara, ropa, iluminación o cambios de exposición. Antes de interpretar los resultados como evidencia de fatiga o estrés, se necesita validación con datos de referencia, población diversa, protocolo controlado, métricas de error y revisión ética/profesional. No uses los resultados para decisiones clínicas, de seguridad o de misión.
