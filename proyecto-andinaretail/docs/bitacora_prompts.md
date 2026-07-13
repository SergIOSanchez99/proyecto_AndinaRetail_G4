Prompts
**Prompt DE Generación de Datos**

Actúa como ingeniero de datos senior especializado en generación de datos sintéticos para proyectos de analítica de datos.

Genera un único script en Python 3.11 llamado generar_datos.py que cree datos sintéticos para la empresa ficticia AndinaRetail S.A.C., una empresa peruana de retail omnicanal con tiendas físicas y canal digital.

El script debe usar pandas, numpy, random, pathlib y Faker con locale 'es_PE'. Debe ser completamente reproducible, por lo que debes fijar las semillas:

numpy.random.seed(2026)
random.seed(2026)
Faker.seed(2026)

El script debe crear automáticamente una carpeta llamada datos/ y exportar los siguientes archivos CSV en formato UTF-8:

1. tiendas.csv

Debe contener 12 tiendas con los siguientes campos:

* id_tienda
* nombre
* ciudad: Lima, Arequipa, Trujillo, Cusco o Piura
* region
* tipo: Física o Virtual
* area_m2
* fecha_apertura

Considera que debe existir al menos una tienda virtual y tiendas físicas distribuidas entre las cinco ciudades.

2. productos.csv

Debe contener 800 productos con los siguientes campos:

* id_producto
* nombre
* categoria: Abarrotes, Bebidas, Limpieza, Cuidado Personal, Electrohogar u Hogar
* subcategoria
* marca
* precio_lista
* costo_unitario
* fecha_alta

El costo_unitario debe estar entre el 60% y 80% del precio_lista. Los precios deben variar de forma realista según la categoría; por ejemplo, Electrohogar debe tener precios más altos que Abarrotes o Bebidas.

3. clientes.csv

Debe contener 15 000 clientes ficticios con los siguientes campos:

* id_cliente
* nombre
* edad
* genero
* ciudad
* distrito
* fecha_registro
* canal_preferido: Tienda, Web o App
* segmento
* fecha_ultima_compra
* frecuencia_compras
* dias_desde_ultima_compra
* churn

La edad debe seguir una distribución aproximadamente normal con media 38 y desviación estándar 12, truncada entre 18 y 80 años.

Las fechas de registro deben estar entre 2022 y 2025.

Todos los nombres deben ser ficticios y generados con Faker; no uses datos reales.

El campo churn debe calcularse tomando como fecha de corte el 2025-12-31. Un cliente tendrá churn = 1 si no realizó compras en los últimos 90 días, y churn = 0 en caso contrario.

La probabilidad de churn debe aumentar cuando el cliente tiene baja frecuencia histórica de compras y una última compra antigua.

4. ventas.csv

Debe contener aproximadamente 250 000 líneas de venta entre el 2023-01-01 y el 2025-12-31, con los siguientes campos:

* id_venta
* fecha
* id_cliente
* id_tienda
* id_producto
* cantidad
* precio_unitario
* descuento_pct
* costo_unitario
* monto_total
* margen_unitario
* margen_total
* canal: Tienda, Web o App
* metodo_pago

La cantidad debe estar principalmente entre 1 y 8 unidades, con mayor probabilidad de valores 1 y 2. Se pueden incluir algunos outliers controlados de cantidad.

El campo descuento_pct debe almacenarse como decimal entre 0.00 y 0.35. Por ejemplo, 0.10 representa 10%.

El monto_total debe calcularse como:

cantidad * precio_unitario * (1 - descuento_pct)

El costo_unitario debe provenir del producto vendido.

El margen_unitario debe calcularse como:

precio_unitario * (1 - descuento_pct) - costo_unitario

El margen_total debe calcularse como:

monto_total - (cantidad * costo_unitario)

El canal debe ser coherente con el tipo de tienda, pero también debe reflejar el crecimiento del canal digital en el tiempo.

5. inventario.csv

Debe contener snapshots mensuales por producto y tienda desde enero de 2023 hasta diciembre de 2025, con los siguientes campos:

* id_producto
* id_tienda
* periodo en formato AAAA-MM
* stock_inicial
* unidades_vendidas
* reabastecimiento
* stock_final
* costo_almacenamiento_unitario
* costo_almacenamiento_total

El stock_final debe calcularse de forma coherente a partir del stock_inicial, unidades_vendidas y reabastecimiento.

El costo_almacenamiento_total debe calcularse como:

stock_final * costo_almacenamiento_unitario

Además, el script debe incorporar obligatoriamente los siguientes patrones de negocio:

1. Estacionalidad

Deben existir picos de ventas en julio por Fiestas Patrias.

Deben existir picos de ventas en diciembre por Navidad.

El canal digital, especialmente Web y App, debe crecer progresivamente entre 2023 y 2025.

2. Patrón diagnóstico de margen

A partir del segundo trimestre de 2025, las tiendas de Trujillo deben mostrar una caída de margen.

Esta caída debe explicarse por mayor descuento promedio y mayor costo de almacenamiento.

El patrón debe ser suficientemente visible para poder analizarlo en una etapa descriptiva y diagnóstica.

3. Churn o inactividad

Un cliente se considera inactivo si no realizó compras en los últimos 90 días tomando como fecha de corte el 2025-12-31.

La probabilidad de inactividad debe aumentar cuando el cliente tiene baja frecuencia histórica de compra y una última compra antigua.

Los datos deben permitir entrenar posteriormente un modelo de clasificación para predecir churn.

4. Demanda predecible

La cantidad vendida debe depender de la categoría, el mes, el canal y el descuento.

Debe existir ruido aleatorio moderado para que los datos no sean artificialmente perfectos.

Los datos deben permitir construir modelos predictivos de demanda por categoría y periodo.

5. Calidad de datos

Incluir entre 1% y 3% de valores faltantes en campos seleccionados, como metodo_pago, descuento_pct, canal_preferido o distrito.

Incluir algunos outliers controlados en variables como cantidad, descuento_pct o monto_total.

Los outliers no deben romper la coherencia general del dataset, pero deben exigir limpieza y preparación de datos.

También debes generar automáticamente un archivo data_dictionary.md dentro de la carpeta datos/. Este archivo debe describir:

* Nombre de cada tabla
* Descripción de cada tabla
* Campo
* Tipo de dato
* Descripción
* Dominio o valores permitidos
* Observaciones importantes
* Patrones sintéticos incorporados

Requisitos adicionales del script:

* El código debe estar ordenado en funciones.
* Debe incluir comentarios claros.
* Debe imprimir al final un resumen con la cantidad de registros generados por cada CSV.
* Debe validar que no existan claves foráneas inválidas entre ventas, clientes, tiendas y productos.
* Debe validar que monto_total, margen_total, stock_final y costo_almacenamiento_total sean coherentes.
* Debe validar que los volúmenes generados estén dentro de los rangos solicitados.
* Debe validar que existan picos de ventas en julio y diciembre.
* Debe validar que el canal digital crezca entre 2023 y 2025.
* Debe validar que Trujillo tenga caída de margen desde 2025-Q2.
* Debe validar que existan entre 1% y 3% de valores faltantes en los campos seleccionados.
* No debe usar datos reales de personas o empresas.
* No debe depender de archivos externos.
* El resultado debe poder ejecutarse directamente con:

python generar_datos.py

Entrega únicamente el código completo del archivo generar_datos.py. El script debe encargarse de crear los CSV y el archivo data_dictionary.md automáticamente.

**Prompt Notebook?Estadistica**
Actúa como analista estadístico senior apoyando un proyecto de analítica de datos en Python (Jupyter). Tengo 5 datasets sintéticos de una empresa de retail (tiendas, productos, clientes, ventas, inventario) y necesito construir el notebook 01_estadistica.ipynb. 
Ayúdame a: 
(1) cargar y explorar la estructura de los datos, cuantificando valores faltantes y determinando si son aleatorios o informativos; 
(2) detectar outliers con el método IQR en variables clave (monto, cantidad, precio, edad) y determinar si corresponden a comportamiento legítimo del negocio o errores de generación, cruzando con variables categóricas como apoyo; 
(3) calcular estadística descriptiva completa (tendencia central, dispersión, asimetría, curtosis); 
(4) construir tablas de frecuencia y visualizaciones univariadas/bivariadas, incluyendo una matriz de correlación; 
(5) formular y contrastar al menos 3 hipótesis de negocio con las pruebas adecuadas (t-test, ANOVA, chi-cuadrado), verificando explícitamente sus supuestos (normalidad, homogeneidad de varianzas, frecuencias esperadas) e interpretando los resultados aunque los supuestos no se cumplan perfectamente; 
(6) calcular intervalos de confianza de 95% para los indicadores más relevantes. Documenta cada sección con celdas Markdown de objetivo, método, resultado e interpretación de negocio, y cierra con conclusiones accionables para la Gerencia.

**Prompt Notebook descriptivo_diagnostico**
Actúa como analista de datos senior apoyando el mismo proyecto de retail. Necesito construir el notebook 02_descriptivo_diagnostico.ipynb a partir de las mismas 5 tablas sintéticas (ya sé que hay una tabla de ventas con costo y margen ya calculados). 
Ayúdame a: 
(1) construir series de tiempo mensuales de ventas, identificar estacionalidad por mes del calendario, y analizar la evolución de la participación del canal digital frente al físico a lo largo de los años; 
(2) hacer un análisis de Pareto 80/20 para productos, clientes y categorías, e interpretar qué tan concentrado o disperso está cada uno; 
(3) construir una segmentación RFM (Recencia, Frecuencia, Valor Monetario) con scores por quintiles y segmentos de negocio interpretables (Campeones, En riesgo, Hibernando, etc.), usando como fecha de referencia el último día del dataset; complementarla con un clustering K-Means sobre las mismas variables estandarizadas, usando el método del codo para elegir k, y comparar ambos enfoques; 
(4) hacer un diagnóstico de causa raíz de la caída de margen reportada en una de las ciudades: identificar en qué plaza y periodo se concentra, comparar cohortes antes/después mediante drill-down, y descomponer la variación evaluando descuento aplicado y costo de almacenamiento como posibles causas, cruzando ventas con inventario. Documenta cada sección con celdas Markdown de objetivo/método/resultado, y cierra con conclusiones de negocio accionables que conecten con el resto del proyecto (churn para la Parte 3, recomendaciones para la Parte 4).

