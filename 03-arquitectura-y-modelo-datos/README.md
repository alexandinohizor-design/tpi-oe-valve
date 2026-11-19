# 3. Arquitectura Tecnológica y Modelo de Datos

## Arquitectura del Motor de Indexación
El sistema propuesto se integra como una capa intermedia de alto rendimiento entre el *Frontend* del Mercado de la Comunidad de Steam y los Servidores de Inventario de Valve:
* **Ingesta y Parseo:** Lectura de definiciones de activos digitales en formatos binarios/estructurados (**Protobuf / VDF**) provenientes de la *Steam Web API* y servidores de juego.
* **Almacenamiento en Memoria (Redis):** Indexación de claves compuestas por tipo de ítem y atributos técnicos (*Float Value*, *Pattern ID*, desgaste y pegatinas) para búsquedas en milisegundos.
* **Control Transaccional:** Uso de bloqueos atómicos (`SET NX`) para evitar condiciones de carrera ante compras concurrentes sobre un mismo activo único.

## Entidades Principales del Modelo de Datos
* **`ITEM_ACTIVO`:** `asset_id` (PK), `class_id`, `instance_id`, `owner_steam_id`, `float_value`, `pattern_seed`, `estado_bloqueo`.
* **`PUBLICACION_MERCADO`:** `listing_id` (PK), `asset_id` (FK), `vendedor_steam_id`, `precio_lista`, `comision_valve`, `estado_publicacion`.
* **`TRANSACCION_WALLET`:** `tx_id` (PK), `listing_id` (FK), `comprador_steam_id`, `monto_debitado`, `timestamp`, `estado_tx` (`PENDIENTE`, `COMPLETADA`, `REVERTIDA`).
