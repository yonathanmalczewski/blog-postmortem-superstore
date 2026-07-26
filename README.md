# Post-Mortem: Dashboard Comercial de Superstore

## Contexto
El proyecto consistía en el desarrollo de un Dashboard comercial integral para el análisis de ventas de la empresa Superstore. El objetivo principal era automatizar el modelado y la visualización de datos mediante funciones lógicas y de búsqueda avanzadas, proporcionando a los diferentes equipos métricas precisas y actualizadas para la toma de decisiones estratégicas.

## Problema
Durante la integración final del panel, experimentamos un fallo técnico que afectó la integridad visual de los datos. La implementación simultánea de validaciones de datos complejas para restringir porcentajes y el uso de múltiples funciones anidadas (como `BUSCARX` y `SUMAR.SI.CONJUNTO`) generó un cuello de botella en el procesamiento. Este conflicto provocó que las reglas de formato condicional fallaran, mostrando datos desfasados y porcentajes erróneos en el panel principal durante una revisión clave con los stakeholders. Esto representó un riesgo temporal para la confianza del equipo en las métricas presentadas.
