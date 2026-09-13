¿Por qué es mala práctica usar SELECT *?
Aunque SELECT * es cómodo para explorar una tabla rápidamente en el día a día, en consultas reales, reportes o producción se considera una mala práctica:
1.	Rendimiento y consumo de recursos innecesario: Trae todas las columnas de la tabla (incluso campos pesados como textos largos, descripciones o identificadores internos). Esto satura la memoria del servidor y el ancho de banda de red.
2.	Consultas frágiles (rompe reportes y aplicaciones): Si alguien agrega, elimina o cambia el orden de las columnas en la tabla original, las vistas, dashboards o scripts en Python/Power BI que dependen de esa consulta pueden romperse o desalinearse.
3.	Poco declarativo: Al leer la consulta, no queda claro qué datos se necesitan realmente para responder la pregunta de negocio.
4.	Impide el uso óptimo de índices: Si el motor de base de datos solo necesita 2 columnas y ambas están en un índice (covering index), con SELECT * se ve obligado a leer la tabla entera en disco.

¿Por qué son importantes los alias (AS) para un stakeholder no técnico?
Un stakeholder (gerente, líder de producto, equipo comercial) no conoce ni tiene por qué interpretar los nombres técnicos o abreviaciones que se usan en las bases de datos.
1.	Claridad inmediata del negocio: Transforma nombres crudos de base de datos en lenguaje claro.
2.	Evita columnas sin nombre en cálculos: Cuando hacés agregaciones o cálculos (SUM(precio * cantidad) o DATEDIFF(...)), SQL devuelve la columna como (Sin nombre de columna) o column_1. Sin un alias (AS Total_Facturado), el stakeholder no sabe qué número está mirando.
3.	Ahorra retrabajo en visualizaciones: Si entregás una consulta con buenos alias, el archivo CSV, Excel o reporte en Power BI ya queda listo para leer sin necesidad de renombrar manualmente cada columna.
Por ejemplo, se podría transformar la columna “total_amount” en una que diga “monto_total” o incluso, se podría especificar el monto total de qué es, por ejemplo, “monto_total_ventas”.
