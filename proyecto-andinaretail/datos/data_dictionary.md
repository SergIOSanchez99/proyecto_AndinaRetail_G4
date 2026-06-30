
# Diccionario de datos - AndinaRetail S.A.C.

## Descripción general

Los datos corresponden a una empresa ficticia peruana de retail omnicanal llamada AndinaRetail S.A.C.
Todos los registros son sintéticos y fueron generados mediante un script reproducible en Python usando semillas fijas.

El conjunto de datos permite desarrollar análisis estadístico, descriptivo, diagnóstico, predictivo, prescriptivo y tableros de control.

---

## Tabla: tiendas.csv

Descripción: contiene información maestra de las tiendas físicas y del canal virtual de AndinaRetail.

| Campo | Tipo de dato | Descripción | Dominio / valores permitidos | Observaciones |
|---|---|---|---|---|
| id_tienda | entero | Identificador único de tienda | 1 a 12 | Clave primaria |
| nombre | texto | Nombre ficticio de la tienda | Texto | No corresponde a una empresa real |
| ciudad | texto | Ciudad donde opera la tienda | Lima, Arequipa, Trujillo, Cusco, Piura | Incluye cobertura nacional para el canal virtual |
| region | texto | Región comercial asociada | Costa Centro, Norte, Sur, Sur Andino, Nacional | Variable descriptiva |
| tipo | texto | Tipo de tienda | Física, Virtual | El canal Web/App se asocia a tienda virtual |
| area_m2 | entero | Área aproximada de la tienda | 0 o valores positivos | La tienda virtual tiene área 0 |
| fecha_apertura | fecha | Fecha de apertura de la tienda | YYYY-MM-DD | Valor sintético |

---

## Tabla: productos.csv

Descripción: contiene el catálogo sintético de productos.

| Campo | Tipo de dato | Descripción | Dominio / valores permitidos | Observaciones |
|---|---|---|---|---|
| id_producto | entero | Identificador único del producto | 1 a 800 | Clave primaria |
| nombre | texto | Nombre ficticio del producto | Texto | Compuesto por subcategoría, marca ficticia y código |
| categoria | texto | Categoría comercial | Abarrotes, Bebidas, Limpieza, Cuidado Personal, Electrohogar, Hogar | Usada para análisis de ventas y demanda |
| subcategoria | texto | Subgrupo de producto | Depende de la categoría | Variable de detalle |
| marca | texto | Marca ficticia | Lista de marcas sintéticas | No representa marcas reales |
| precio_lista | decimal | Precio base del producto | Valores positivos | Varía por categoría |
| costo_unitario | decimal | Costo unitario del producto | 60% a 80% del precio_lista | Usado para calcular margen |
| fecha_alta | fecha | Fecha de alta del producto | 2021 a 2025 | Valor sintético |

---

## Tabla: clientes.csv

Descripción: contiene información sintética de clientes y variables derivadas para análisis de churn.

| Campo | Tipo de dato | Descripción | Dominio / valores permitidos | Observaciones |
|---|---|---|---|---|
| id_cliente | entero | Identificador único del cliente | 1 a 15000 | Clave primaria |
| nombre | texto | Nombre ficticio del cliente | Texto generado con Faker | No corresponde a personas reales |
| edad | entero | Edad del cliente | 18 a 80 | Distribución normal truncada |
| genero | texto | Género sintético | Femenino, Masculino, Otro | Variable demográfica |
| ciudad | texto | Ciudad de residencia | Lima, Arequipa, Trujillo, Cusco, Piura | Usada para análisis territorial |
| distrito | texto | Distrito de residencia | Distritos sintéticos por ciudad | Incluye faltantes controlados |
| fecha_registro | fecha | Fecha de registro del cliente | 2022 a 2025 | Coherente con la primera compra |
| canal_preferido | texto | Canal preferido del cliente | Tienda, Web, App | Incluye faltantes controlados |
| segmento | texto | Segmento comercial derivado | Inactivo, Alto Valor, Frecuente, Ocasional, Regular | Derivado de frecuencia, valor y churn |
| fecha_ultima_compra | fecha | Última fecha de compra del cliente | Fecha o vacío | Derivada de ventas.csv |
| frecuencia_compras | entero | Número de líneas de venta asociadas al cliente | 0 o mayor | Usada en churn |
| dias_desde_ultima_compra | entero | Días desde la última compra al 2025-12-31 | 0 o mayor | Si no compró, toma valor 999 |
| churn | entero | Indicador de inactividad | 1 = inactivo, 0 = activo | Churn = 1 si no compró en los últimos 90 días |

---

## Tabla: ventas.csv

Descripción: contiene líneas sintéticas de venta entre 2023 y 2025.

| Campo | Tipo de dato | Descripción | Dominio / valores permitidos | Observaciones |
|---|---|---|---|---|
| id_venta | entero | Identificador único de línea de venta | 1 a 250000 | Clave primaria |
| fecha | fecha | Fecha de venta | 2023-01-01 a 2025-12-31 | Incluye estacionalidad |
| id_cliente | entero | Cliente que realiza la compra | Debe existir en clientes.csv | Clave foránea |
| id_tienda | entero | Tienda asociada a la venta | Debe existir en tiendas.csv | Clave foránea |
| id_producto | entero | Producto vendido | Debe existir en productos.csv | Clave foránea |
| cantidad | entero | Unidades vendidas | Principalmente 1 a 8 | Incluye outliers controlados |
| precio_unitario | decimal | Precio unitario aplicado | Positivo | Derivado del precio_lista |
| descuento_pct | decimal | Descuento aplicado | 0.00 a 0.35 o faltante | 0.10 representa 10% |
| costo_unitario | decimal | Costo unitario del producto vendido | Positivo | Proviene de productos.csv |
| monto_total | decimal | Importe total de venta | Positivo | cantidad * precio_unitario * (1 - descuento_pct) |
| margen_unitario | decimal | Margen unitario | Puede ser bajo o negativo | precio neto - costo unitario |
| margen_total | decimal | Margen total de la línea | Puede ser bajo o negativo | monto_total - cantidad * costo_unitario |
| canal | texto | Canal de venta | Tienda, Web, App | Web/App crecen entre 2023 y 2025 |
| metodo_pago | texto | Método de pago | Efectivo, tarjetas, Yape, Plin, Transferencia | Incluye faltantes controlados |

---

## Tabla: inventario.csv

Descripción: contiene snapshots mensuales de inventario por producto y tienda.

| Campo | Tipo de dato | Descripción | Dominio / valores permitidos | Observaciones |
|---|---|---|---|---|
| id_producto | entero | Producto inventariado | Debe existir en productos.csv | Clave foránea |
| id_tienda | entero | Tienda inventariada | Debe existir en tiendas.csv | Clave foránea |
| periodo | texto | Periodo mensual | Formato AAAA-MM | Desde 2023-01 hasta 2025-12 |
| stock_inicial | entero | Stock inicial del periodo | 0 o mayor | Snapshot mensual |
| unidades_vendidas | entero | Unidades vendidas en el periodo | 0 o mayor | Derivado de ventas.csv |
| reabastecimiento | entero | Unidades repuestas | 0 o mayor | Generado para cubrir demanda |
| stock_final | entero | Stock final del periodo | 0 o mayor | stock_inicial + reabastecimiento - unidades_vendidas |
| costo_almacenamiento_unitario | decimal | Costo unitario de almacenamiento | Positivo | Aumenta en Trujillo desde 2025-Q2 |
| costo_almacenamiento_total | decimal | Costo total de almacenamiento | Positivo | stock_final * costo_almacenamiento_unitario |

---

## Patrones sintéticos incorporados

1. Estacionalidad:
   - Picos de ventas en julio por Fiestas Patrias.
   - Picos de ventas en diciembre por Navidad.
   - Mayor crecimiento del canal digital entre 2023 y 2025.

2. Patrón diagnóstico:
   - Desde el segundo trimestre de 2025, Trujillo presenta caída de margen.
   - La caída se explica por descuentos más altos y mayor costo de almacenamiento.

3. Churn:
   - Un cliente es inactivo si no compró en los últimos 90 días respecto al 2025-12-31.
   - La inactividad aumenta en clientes con baja frecuencia histórica.

4. Demanda predecible:
   - La cantidad vendida depende de categoría, mes, canal y descuento.
   - Se añade ruido aleatorio moderado.

5. Calidad de datos:
   - Se incorporan faltantes controlados entre 1% y 3%.
   - Se incorporan outliers controlados en cantidad y monto total.
