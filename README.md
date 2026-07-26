# Post-Mortem: Dashboard Comercial de Superstore

## Contexto
El proyecto consistía en el desarrollo de un Dashboard comercial integral para el análisis de ventas de la empresa Superstore. El objetivo principal era automatizar el modelado y la visualización de datos mediante funciones lógicas y de búsqueda avanzadas, proporcionando a los diferentes equipos métricas precisas y actualizadas para la toma de decisiones estratégicas.

## Problema
Durante la integración final del panel, experimentamos un fallo técnico que afectó la integridad visual de los datos. La implementación simultánea de validaciones de datos complejas para restringir porcentajes y el uso de múltiples funciones anidadas (como `BUSCARX` y `SUMAR.SI.CONJUNTO`) generó un cuello de botella en el procesamiento. Este conflicto provocó que las reglas de formato condicional fallaran, mostrando datos desfasados y porcentajes erróneos en el panel principal durante una revisión clave con los stakeholders. Esto representó un riesgo temporal para la confianza del equipo en las métricas presentadas.

## Acciones y Análisis Post-Mortem

**Cronología del Incidente:**
* **10:00 AM:** Se implementa la actualización del Dashboard comercial, integrando las nuevas validaciones de datos para restringir porcentajes y cantidades.
* **10:15 AM:** El equipo de ventas reporta que el panel principal muestra alertas visuales incorrectas; el formato condicional marca en rojo métricas que están dentro de los márgenes aceptables.
* **10:30 AM:** El equipo técnico inicia la investigación y detecta que la combinación de validaciones con funciones lógicas complejas (como `Y`), sumado al procesamiento simultáneo de fórmulas avanzadas (`BUSCARX`, `SUMAR.SI.CONJUNTO`, `PROMEDIO.SI` e `ÍNDICE` con `COINCIDIR`), está generando un desfase en el motor de cálculo.
* **10:45 AM:** Se aplica una mitigación temporal, simplificando el formato condicional para restaurar la lectura de los datos básicos y permitir que el equipo de ventas continúe su labor.

**Análisis de Causas Raíz:**
Tras investigar el incidente, identificamos que la causa principal fue una sobrecarga de procesamiento. La acumulación de funciones de cálculo intensivo operando directamente sobre las reglas de formato condicional causó un desfase. Al validar esto, detectamos que en nuestro entorno de pruebas el volumen de datos era menor, por lo que este cuello de botella no se manifestó antes de la entrega final. 

**Acciones Correctivas y Preventivas:**
* **Acción Inmediata:** Se reestructuraron las reglas del formato condicional. En lugar de procesar las lógicas complejas en tiempo real dentro del panel visual, se crearon columnas auxiliares precalculadas para aligerar la carga del sistema.
* **Acción Preventiva:** Se diseñó un nuevo protocolo de pruebas utilizando volúmenes de datos que simulan escenarios de estrés reales antes de desplegar cualquier nueva versión del Dashboard.
