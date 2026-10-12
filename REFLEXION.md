# Reflexión

- **Equipo:** Tannia Lucia Hernandez
- **Integrante:** Tannia Lucia Hernandez
- **Cohorte:** COH1
- **Features:** cabin_openings, autonomy_handover
- **Video (inglés, menos de 3 minutos):** https://drive.google.com/file/d/1fij02HwgXHyvJI84KQfyPQCPuKApnJ_L/view?usp=sharing
- **Enlace al pull request:** Se añadirá cuando se abra.

## Qué quería resolver

Quería hacer visibles dos acciones que el asistente realiza dentro del simulador: mover ventanas o el techo y transferir el control al modo autónomo. Elegí mostrar el estado con señales periféricas, en lugar de repetir la promesa verbal.

## Qué diseñé

cabin_openings representa el carro desde arriba, ubica las cuatro ventanas y refleja el diagrama según el lado del conductor. El porcentaje aclara cuánto está abierta cada zona. El detalle aparece brevemente y luego se reduce mientras quede una apertura. A/C por sí solo no activa una tarjeta falsa. “Todo cerrado” aparece una vez, en tono neutro. Si el techo está abierto y la cortinilla no está retraída, el dibujo sigue mostrando el techo abierto y lo resalta en ámbar. Cuando la cortinilla se está retirando por completo, su animación termina antes de la del techo.

autonomy_handover usa el perímetro: la etiqueta de autonomía dura tres segundos y después queda un borde tenue; el ámbar aparece durante el aviso breve de tomar el control. Las dos features leen estado y no lo modifican.

## Mi aporte y el uso de IA

Usé Codex para leer la especificación y las APIs, implementar las features, regenerar el bundle y redactar las notas. Yo definí el problema y revisé el diseño frente al guion. Corregí una propuesta de IA que mostraba el vidrio restante en vez del porcentaje de apertura, y ajusté la animación de la cortinilla al revisar la separación entre eventos.

## Prueba y límites

Ejecuté la demo local completa con Reproducir todo y revisé t03, t10, x01 y t13. Tras el modo autónomo, confirmé que podía retomar el manejo con el teclado. Después del último ajuste, una comprobación focal verificó que una carga inicialmente autónoma muestra solo el borde tenue y que una activación nueva conserva la etiqueta breve. No revisé la consola del navegador ni probé visualmente una recarga con autonomía activa. El paso t11 menciona lluvia, pero no cambia el clima del simulador; por eso no afirmo que la reproducción completa haya validado esa alerta. No haré un miniestudio ni presentaré estas pruebas como evidencia de usabilidad general.

La interfaz es una simulación en pantalla, no un tablero certificado. Las animaciones representan el recorrido aunque el estado del simulador cambie de inmediato. Una prueba individual sirve para detectar fallos funcionales y visuales; no demuestra que otras personas entiendan mejor el sistema ni que mejore su conducción. Aprendí que cada confirmación debe coincidir con el estado que realmente se muestra y que tengo que revisar también las interacciones entre features.
