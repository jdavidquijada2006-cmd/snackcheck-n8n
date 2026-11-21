# SnackCheck — Verificador de Nutrición por Código de Barras

## Propósito
Automatización en n8n que recibe un código de barras vía Webhook, consulta los datos nutricionales del producto en Open Food Facts, clasifica su perfil nutricional (Saludable, Moderado o Poco saludable) y genera un veredicto amigable con IA mediante Groq.

## Cómo funciona
1. **Webhook (`POST /nutrition-check`):** Recibe el JSON `{"barcode": "..."}`.
2. **Validación de entrada (`If` / `If1`):** Verifica si el código viene vacío (devuelve `200` con JSON autodocumentante) o si tiene formato inválido (devuelve `400`).
3. **Consulta a Open Food Facts (`HTTP Request`):** Obtiene `product_name`, `nutriscore_grade`, `nutrient_levels` y `nutriments` por código de barras.
4. **Verificación de existencia y datos (`If2` / `If3`):** Devuelve `404` si el producto no existe o `200` (`insufficient_data`) si faltan datos nutricionales.
5. **Clasificación (`Code`):** Evalúa nutrientes altos (`0–3`) y Nutri-Score (`a–e`), aplicando siempre el criterio más estricto entre ambos.
6. **Veredicto IA (`Basic LLM Chain` + `Groq Chat Model`):** Redacta un párrafo breve adaptado al nivel nutricional y lo devuelve en texto plano (`200`).

## Configuración
- Importar `Snackcheck- verificador nutricional.json` en n8n.
- Configurar una credencial de **Groq API** en n8n y vincularla al nodo `Groq Chat Model`.
- Activar el flujo (`Publish`) para habilitar la URL `/webhook/nutrition-check`.

## Limitaciones
- Depende de la disponibilidad y completitud de los datos cargados en Open Food Facts.
- Si un producto carece de Nutri-Score y niveles de nutrientes, el sistema detiene la evaluación para evitar falsos positivos.
