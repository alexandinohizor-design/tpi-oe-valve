# Trabajo Práctico Integrador — Organización Empresarial (UTN FRP)

**Proyecto:** Sistema de Búsqueda e Indexación de Metadatos de Activos Digitales en el Ecosistema Steam  
**Organización Analizada:** Valve Corporation  
**Carrera:** Tecnicatura Universitaria en Programación (TUP) — Universidad Tecnológica Nacional (Facultad Regional Paraná)  
**Autor:** Alex Andino  
**Año Lectivo:** 2026  

--

## Alcance Integral del Proyecto
Este repositorio documenta de manera integrada el desarrollo del Trabajo Práctico Integrador de **Organización Empresarial**, articulando el análisis administrativo con el diseño de sistemas de información:

1. **Enfoque Sistémico, Organigrama y Estructura ([`01-analisis-organizacional/`](./01-analisis-organizacional/README.md)):** Caracterización de Valve Corporation como sistema socio-técnico abierto, contraste entre jerarquías tradicionales y autoorganización (*flatland* / *cabals*), organigrama formal adaptado a la cátedra y delimitación de supuestos académicos.
2. **Planificación y Control de Gestión ([`02-planificacion-y-control/`](./02-planificacion-y-control/README.md)):** Transformación de metas cuantificables en indicadores de desempeño con fórmulas, estándares, responsables, fuentes de datos, frecuencias y acciones correctivas ante desvíos.
3. **Arquitectura Tecnológica y Modelo de Datos ([`03-arquitectura-y-modelo-datos/`](./03-arquitectura-y-modelo-datos/README.md)):** Diseño lógico del motor de indexación de metadatos (*Float Value*, *Pattern ID*) sobre caché **Redis** y parseo de estructuras **Protobuf/VDF**.
4. **Modelado de Procesos BPMN 2.0 y Casos de Uso ([`04-procesos-bpmn-y-casos-uso/`](./04-procesos-bpmn-y-casos-uso/README.md)):** Diagrama BPMN 2.0 con separación de *Pools*, *Flujos de Mensaje*, subprocesos, control de concurrencia mediante bloqueo atómico en Redis y *Rollback* en *Steam Wallet*, junto con los casos de uso `CU-01` y `CU-02`.
5. **Gestión Ágil del Proyecto (GitHub Projects):** Tablero Kanban con Historias de Usuario, criterios de aceptación y seguimiento de estados.

---

## Análisis Crítico del Uso de Inteligencia Artificial (Gemini)

Durante la elaboración y revisión del Trabajo Práctico Integrador se utilizó **Google Gemini exclusivamente como herramienta de consulta, guía metodológica y apoyo para validar sintaxis y redacción**. La concepción del proyecto, el diseño organizacional, la lógica de negocio y la construcción de cada artefacto fueron realizados íntegramente por el autor.

A continuación, se documentan ejemplos concretos de consultas realizadas a la herramienta, las sugerencias obtenidas y las decisiones críticas aplicadas por el autor:

### Ejemplo 1: Consulta metodológica sobre notación BPMN 2.0
* **Prompt utilizado (consulta):** *"¿Qué reglas de notación BPMN 2.0 debo respetar al vincular un cliente externo con los sistemas internos de Valve (caché Redis y Steam Wallet) y cómo se representan las excepciones por compras simultáneas?"*
* **Respuesta orientativa obtenida:** La herramienta sugirió utilizar carriles diferenciados para los componentes internos (*Frontend*, *Motor de Indexación*, *Servidores de Inventario* y *Pasarela de Pagos*), pero ofreció una explicación genérica que no contemplaba el aislamiento formal entre entidades externas e internas ni el manejo explícito de condiciones de carrera.
* **Criterio y elaboración del autor:** A partir de la consulta, el autor diseñó y construyó el diagrama separando formalmente ambos *Pools* (`Usuario Comprador` y `Valve Corporation`) vinculados exclusivamente mediante *Flujos de Mensaje* discontinuos, estructurando dos subprocesos e incorporando un bloqueo atómico en Redis previo al cobro junto con una rutina de *Rollback* ante fallos de transferencia.

### Ejemplo 2: Guía de estructuración de indicadores de control de gestión
* **Prompt utilizado (consulta):** *"¿Qué elementos formales exige la teoría de control de gestión para convertir una meta cuantificable de latencia y disponibilidad en un indicador operativo completo?"*
* **Respuesta orientativa obtenida:** El asistente enumeró componentes teóricos generales (métrica, objetivo y frecuencia), acompañados de ejemplos técnicos básicos de infraestructura que carecían de asignación de responsabilidades organizacionales, fuentes verificables y protocolos ante desvíos.
* **Criterio y elaboración del autor:** Tomando esa guía estructural, el autor definió y redactó cada indicador de la matriz adaptándolo al caso de estudio de Valve, estableciendo fórmulas matemáticas propias, estándares objetivo, fuentes de telemetría (logs de Redis/API), responsables por área y acciones correctivas concretas.

### Valoración Crítica
El uso de IA como instancia de consulta permitió agilizar la revisión de formato Markdown, contrastar alternativas de redacción y detectar posibles ambigüedades antes de la entrega. No obstante, cada sugerencia fue sometida a validación técnica y académica por parte del autor para garantizar rigor en la notación BPMN 2.0 y coherencia con los contenidos de la asignatura.
