# toDus Desktop

Cliente de escritorio de toDus para Windows. La aplicacion se distribuye **unicamente como binario** a traves de Releases.

## Descarga

[Ultima version](https://github.com/Daro-IR/todus-desktop/releases/latest)

## Actualizaciones

La app comprueba automaticamente `Daro-IR/todus-desktop` al iniciar y desde **Ajustes > Buscar actualizaciones**. Los instaladores y el manifiesto `latest.yml` se publican en Releases.

## Fox Premium

- Licencia sin conexion de 30 dias, con prueba automatica de 10 dias en la primera instalacion.
- Compra dentro de la app con QR de Transfermovil y EnZona, y canje manual o automatico del codigo.
- **Cola de transferencias** persistente: hasta 2 subidas y 2 descargas a la vez, con reintentos.
- Arrastrar archivos al chat y fragmentacion automatica en zip de hasta 145 MB con verificacion SHA-256.
- **Mis subidas**: todas las subidas de la cola van a un grupo privado propio; el boton `+` de la cabecera anade archivos y el gestor guarda el historial (cola y adjuntos normales).
- **Listas .txt compartibles**: selecciona algunas o todas las subidas y genera un `.txt` con nombre, tamano, SHA-256 y enlaces; guardalo o compartelo por toDus.
- **Importar listas**: el gestor de descargas interpreta el formato nuevo, el antiguo `tdf_partes=1` y listas simples de URLs.

Sin Fox Premium la app sigue funcionando con normalidad: solo se bloquean esas tres funciones.

Las URLs de las listas son enlaces firmados del servidor de toDus y pueden caducar; genera una lista nueva si dejan de responder.

## Fiabilidad

- Cola saliente persistente para mensajes: si se corta la conexion, se reintenta sin duplicar.
- Las llamadas entrantes viejas o reenviadas por la cola offline ya no suenan al iniciar la app.

## Estado

- Version actual: **1.1.0**
- Plataforma: Windows x64 (instalador NSIS)
- Icono: toDusFox

---

(c) Dario. Todos los derechos reservados. Este repositorio solo contiene la documentacion y los binarios de distribucion; el codigo fuente se conserva en un repositorio privado.