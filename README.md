# FORA — prototipo de cámara

Prototipo web experimental para probar en el navegador:

- Conteo aproximado de pestañeadas mediante MediaPipe Face Landmarker.
- Estimación experimental de respiración a partir del desplazamiento aparente de una región del torso.
- Promedio RGB de pequeñas regiones bajo los ojos, mostrado sin clasificar ni interpretar como medida de fatiga.

## Ejecutar localmente

La cámara requiere un contexto seguro (`localhost` o HTTPS). Desde la raíz del repositorio:

```bash
python -m http.server 8000
```

Abre <http://localhost:8000>, concede permiso de cámara y pulsa **Iniciar cámara**. Se necesita conexión a internet para cargar MediaPipe y su modelo desde CDN. También puede publicarse como sitio estático, por ejemplo con GitHub Pages; el acceso a cámara requiere HTTPS.

## Encuadre

Para probar el módulo respiratorio, coloca el rostro en la mitad superior y el torso/pecho visible en la parte inferior. El rectángulo azul indica la región que se intenta seguir. Si el torso no entra en el encuadre, no se podrá calcular una estimación útil.

## Límites y privacidad

Es una demostración, no un dispositivo médico ni un sistema de aptitud operacional. El estimador respiratorio es exploratorio y puede confundir respiración con movimiento corporal, cambios de iluminación, ropa o movimiento de cámara. El umbral de parpadeo puede variar entre personas y condiciones. El valor RGB bajo los ojos cambia con iluminación, exposición y cámara; no diagnostica ojeras ni fatiga.

El código no graba ni envía vídeo: el análisis se ejecuta en el navegador. La descarga inicial de MediaPipe/modelo requiere internet. Para decisiones de salud u operación, no uses estas salidas; se necesita validación adecuada y supervisión profesional.
