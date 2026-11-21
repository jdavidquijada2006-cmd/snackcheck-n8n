# Changelog

## - 2026-11-21
### Added
- Diagrama de arquitectura y rutas de error en Excalidraw (`diagrama-snackcheck.png`).
- Flujo principal en n8n con `Webhook POST /nutrition-check` y respuestas estructuradas (`Respond to Webhook`).
- Validaciones de entrada vacía (`200`), formato inválido (`400`), producto no encontrado (`404`) y datos insuficientes (`200`).
- Lógica de clasificación nutricional combinando semáforo de nutrientes y Nutri-Score en nodo `Code`.
- Generación de veredicto nutricional dinámico mediante Groq (`llama-3.3-70b-versatile`).
