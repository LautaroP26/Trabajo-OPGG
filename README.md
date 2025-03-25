# 🤖 Trabajo OPGG - Flujo de los Bots

## 📌 Descripción
Este sistema de automatización consta de tres bots principales interconectados:
1. **BOT_Abuelo**: Controla el flujo de ejecución de los bots secundarios.
2. **Bot_opgg**: Extrae información de la web de OPGG.
3. **Enviar_Mail**: Envía por correo los resultados obtenidos.

Estos bots trabajan en conjunto para automatizar la extracción de información de jugadores de OPGG y enviar los datos recopilados mediante correo electrónico.

---

## 🔄 Flujo de los Bots
1. **BOT_Abuelo (Orquestador Principal)**
   - Obtiene la fecha actual.
   - Abre un archivo Excel (`busqueda.xlsx`) donde se almacenan los datos.
   - Cuenta el número de filas en el archivo para verificar que hay datos disponibles.
   - Extrae los nombres de los jugadores a buscar en OPGG.
   - Lanza la ejecución del bot **Bot_opgg**.
   - Guarda el archivo Excel actualizado.
   - Ejecuta el bot **Enviar_Mail** para enviar los resultados.

2. **Bot_opgg (Extracción de Datos)**
   - Abre la página web de OPGG.
   - Espera que la página cargue correctamente.
   - Itera sobre cada jugador a buscar.
   - Busca el nombre del jugador y extrae información relevante como puntaje.
   - Guarda los datos en el archivo Excel.
   - Cierra el navegador una vez completada la búsqueda.

3. **Enviar_Mail (Envío de Resultados)**
   - Establece conexión con la cuenta de correo.
   - Verifica si la conexión es exitosa.
   - Si la conexión falla, registra un error en un archivo de log.
   - Si la conexión es exitosa:
     - Adjunta el archivo Excel con los resultados.
     - Envía un correo al destinatario configurado.
     - Cierra la conexión de correo.

---

## 📦 Módulos Utilizados
- `AdvancedExcel` (Versión: 34.37.21 → Última: 34.39.28) → Manipulación de archivos Excel.
- `gmail_` (Versión: 1.12.7 → Última: 1.12.8) → Envío de correos electrónicos.
- `web` → Automatización de interacciones con páginas web.
- `system` → Manejo de variables y procesos internos.

---

## 📌 Consideraciones
- **Estructura Jerárquica:**
  - **BOT_Abuelo** es el bot principal y gestiona las ejecuciones de los bots secundarios.
  - **Bot_opgg** extrae los datos de la web y los almacena.
  - **Enviar_Mail** finaliza el proceso enviando los resultados.
- **Dependencia de la Página Web:** Si OPGG cambia su estructura, el bot puede dejar de funcionar.
- **Seguridad:** La información de acceso al correo está en las variables del sistema y debe mantenerse segura.
- **Registro de Errores:** Si ocurre un fallo, se guarda en un archivo log.
- **Validación de Datos:** Se recomienda verificar que los datos extraídos sean correctos antes de enviarlos.

---

## ⚠️ Limitaciones
- **Falta de Reintentos:** Si una extracción o envío falla, no hay un mecanismo de reintento automático.
- **Formato Fijo:** El archivo Excel tiene un formato predefinido y no se adapta dinámicamente a cambios en los datos.
- **Ejecución Secuencial:** Si un bot falla, el flujo de trabajo se interrumpe completamente.
- **Carga Manual del Archivo:** El archivo Excel debe existir antes de la ejecución.

---

## 🚀 Futuras Mejoras
- Implementar un sistema de reintentos en caso de errores.
- Agregar un mecanismo de validación de datos antes del envío.
- Mejorar la captura de logs para detectar errores con más precisión.
- Automatizar la creación del archivo Excel si no existe.
- Implementar un sistema de notificaciones en caso de fallos críticos.

---

## 📜 Créditos
Desarrollado por **Lautaro Pedernera** como parte del curso de RocketBot de **Marcela Vergara**.

Agradecimientos especiales a **BotSolutions** por su apoyo en la finalización de este proyecto.
