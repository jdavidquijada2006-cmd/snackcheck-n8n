# Registro de Pruebas — SnackCheck

| ID | Escenario | Entrada (`POST /nutrition-check`) | Código HTTP | Resultado Esperado | Estado |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-001** | Producto poco saludable (Nutella) | `{"barcode": "3017620422003"}` | `200` | Veredicto cauteloso en texto plano (Nutri-Score E / alto azúcar y grasas). | PASS |
| **TC-002** | Producto saludable (Copos de avena) | `{"barcode": "3229820129488"}` | `200` | Veredicto alentador en texto plano (Nutri-Score A). | PASS |
| **TC-003** | Producto inexistente | `{"barcode": "9999999999999"}` | `404` | JSON de error indicando producto no encontrado. | PASS |
| **TC-004** | Código vacío o inválido | `{}` / `{"barcode": "abc123"}` | `200` / `400` | JSON autodocumentante (`200`) o error de formato (`400`). | PASS |
