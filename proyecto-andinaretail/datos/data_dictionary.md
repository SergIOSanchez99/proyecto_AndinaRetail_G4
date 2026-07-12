
# Diccionario de datos - AndinaRetail S.A.C.

## Descripción general

Los datos corresponden a una empresa ficticia peruana de retail omnicanal llamada AndinaRetail S.A.C.

Todos los registros son sintéticos y fueron generados mediante un script reproducible en Python con semillas fijas.

El conjunto de datos permite desarrollar análisis estadístico, descriptivo, diagnóstico, predictivo, prescriptivo y tableros de control.

---

## Tabla: tiendas.csv

Descripción: contiene información maestra de las tiendas físicas y del canal virtual.

| Campo | Tipo de dato | Descripción | Dominio / valores permitidos | Observaciones |
|---|---|---|---|---|
| id_tienda | entero | Identificador único de tienda | 1 a 12 | Clave primaria |
| nombre | texto | Nombre ficticio de tienda | Texto | No corresponde a una empresa real |
| ciudad | texto | Ciudad de operación | Lima, Arequipa, Trujillo, Cusco, Piura | La tienda virtual figura con ciudad Lima y región Nacional |
| region | texto | Región comercial | Costa Centro, Norte, Sur, Sur Andino, Nacional | Variable descriptiva |
| tipo | texto | Tipo de tienda | Física, Virtual | Web/App se asocian a tienda virtual |
| area_m2 | entero | Área aproximada | 0 o positivo | Tienda virtual tiene área 0 |
| fecha_apertura | fecha | Fecha de apertura | YYYY-MM-DD | Valor sintético |

---

## Tabla: productos.csv

Descripción: catálogo sintético de productos.

| Campo | Tipo de dato | Descripción | Dominio / valores permitidos | Observaciones |
|---|---|---|---|---|
| id_producto | entero | Identificador único de producto | 1 a 1000 | Clave primaria |
| nombre | texto | Nombre ficticio de producto | Texto | Construido con subcategoría, marca ficticia y código |
| categoria | texto | Categoría comercial | 11 categorías | Usada para análisis de demanda |
| subcategoria | texto | Subcategoría | Depende de la categoría | Variable de detalle |
| marca | texto | Marca ficticia | Lista de marcas sintéticas | No representa marcas reales |
| precio_lista | decimal | Precio base | Positivo | Varía por categoría |
| costo_unitario | decimal | Costo unitario | 60% a 80% del precio_lista | Usado para cálculo de margen |
| fecha_alta | fecha | Fecha de alta | 2021 a 2025 | Valor sintético |

---

## Tabla: clientes.csv

Descripción: clientes ficticios y variables derivadas para churn.

| Campo | Tipo de dato | Descripción | Dominio / valores permitidos | Observaciones |
|---|---|---|---|---|
| id_cliente | entero | Identificador único de cliente | 1 a 15000 | Clave primaria |
| nombre | texto | Nombre ficticio | Texto generado con Faker | No corresponde a personas reales |
| edad | entero | Edad | 18 a 80 | Distribución normal truncada |
| genero | texto | Género sintético | Femenino, Masculino, Otro | Variable demográfica |
| ciudad | texto | Ciudad de residencia | Lima, Arequipa, Trujillo, Cusco, Piura | Usada para análisis territorial |
| distrito | texto | Distrito de residencia | Distritos por ciudad | Incluye faltantes controlados |
| fecha_registro | fecha | Fecha de registro | 2022 a 2025 | Ajustada para no ser posterior a primera compra |
| canal_preferido | texto | Canal preferido | Tienda, Web, App | Incluye faltantes controlados |
| segmento | texto | Segmento comercial | Inactivo, Alto Valor, Frecuente, Ocasional, Regular | Derivado de frecuencia, valor y churn |
| fecha_ultima_compra | fecha | Última compra | Fecha o vacío | Derivada de tickets.csv |
| frecuencia_tickets | entero | Cantidad de tickets del cliente | 0 o mayor | Usada para churn y segmentación |
| frecuencia_lineas | entero | Cantidad de líneas compradas | 0 o mayor | Derivada de ventas.csv |
| valor_total | decimal | Valor total comprado | 0 o mayor | Suma de monto_ticket |
| dias_desde_ultima_compra | entero | Días desde última compra | 0 o mayor | Respecto al 2025-12-31 |
| churn | entero | Indicador de inactividad | 1 = inactivo, 0 = activo | Churn = 1 si no compró en últimos 90 días |

---

## Tabla: tickets.csv

Descripción: cabecera de compra. Cada ticket representa una compra completa y puede tener una o varias líneas en ventas.csv.

| Campo | Tipo de dato | Descripción | Dominio / valores permitidos | Observaciones |
|---|---|---|---|---|
| id_ticket | texto | Identificador único del ticket | T000001 en adelante | Clave primaria |
| fecha | fecha | Fecha de compra | 2023-01-01 a 2025-12-31 | Incluye estacionalidad y campañas |
| id_cliente | entero | Cliente comprador | Debe existir en clientes.csv | Clave foránea |
| id_tienda | entero | Tienda asociada | Debe existir en tiendas.csv | Clave foránea |
| canal | texto | Canal de compra | Tienda, Web, App | Web/App crecen entre 2023 y 2025 |
| metodo_pago | texto | Método de pago | Efectivo, tarjetas, Yape, Plin, Transferencia | Incluye faltantes controlados |
| campaña | texto | Campaña comercial asociada | Normal, Campaña Escolar, Día de la Madre, Día del Padre, Fiestas Patrias, Cyber Wow Abril, Cyber Wow Julio, Cyber Wow Noviembre, Black Friday, Navidad | Derivada de la fecha |
| es_campaña | entero | Indicador de campaña | 1 = campaña, 0 = normal | Derivada de campaña |
| tipo_campaña | texto | Agrupación de campaña | Regular, Escolar, Familiar, Digital, Festiva | Variable analítica |
| cantidad_lineas | entero | Cantidad de líneas del ticket | 1 a 6 | Variable realista |
| unidades_totales | entero | Total de unidades compradas | 1 o mayor | Suma de cantidad en ventas.csv |
| monto_ticket | decimal | Monto total del ticket | Positivo | Suma de monto_total |
| descuento_promedio_ticket | decimal | Descuento promedio del ticket | 0.00 a 0.35 | Promedio de descuentos de líneas |
| margen_ticket | decimal | Margen total del ticket | Puede ser bajo o negativo | Suma de margen_total |

---

## Tabla: ventas.csv

Descripción: detalle de productos comprados dentro de cada ticket.

| Campo | Tipo de dato | Descripción | Dominio / valores permitidos | Observaciones |
|---|---|---|---|---|
| id_venta | entero | Identificador único de línea | 1 en adelante | Clave primaria |
| id_ticket | texto | Ticket asociado | Debe existir en tickets.csv | Clave foránea |
| fecha | fecha | Fecha de venta | 2023-01-01 a 2025-12-31 | Heredada del ticket |
| id_cliente | entero | Cliente comprador | Debe existir en clientes.csv | Heredado del ticket |
| id_tienda | entero | Tienda asociada | Debe existir en tiendas.csv | Heredado del ticket |
| id_producto | entero | Producto vendido | Debe existir en productos.csv | Clave foránea |
| cantidad | entero | Unidades vendidas | Principalmente 1 a 8 | Incluye outliers controlados |
| precio_unitario | decimal | Precio aplicado | Positivo | Derivado del precio_lista |
| descuento_pct | decimal | Descuento aplicado | 0.00 a 0.35 o faltante | 0.10 representa 10% |
| costo_unitario | decimal | Costo del producto | Positivo | Proviene de productos.csv |
| monto_total | decimal | Monto de la línea | Positivo | cantidad * precio_unitario * (1 - descuento_pct) |
| margen_unitario | decimal | Margen unitario | Puede ser bajo o negativo | Precio neto - costo unitario |
| margen_total | decimal | Margen total de línea | Puede ser bajo o negativo | monto_total - cantidad * costo_unitario |
| canal | texto | Canal de venta | Tienda, Web, App | Heredado del ticket |
| metodo_pago | texto | Método de pago | Según canal o faltante | Heredado del ticket |
| campaña | texto | Campaña comercial | Valores definidos en tickets.csv | Heredado del ticket |
| es_campaña | entero | Indicador de campaña | 1 o 0 | Heredado del ticket |
| tipo_campaña | texto | Tipo de campaña | Regular, Escolar, Familiar, Digital, Festiva | Heredado del ticket |

---

## Tabla: inventario.csv

Descripción: snapshots mensuales de inventario por producto y tienda.

| Campo | Tipo de dato | Descripción | Dominio / valores permitidos | Observaciones |
|---|---|---|---|---|
| id_producto | entero | Producto inventariado | Debe existir en productos.csv | Clave foránea |
| id_tienda | entero | Tienda inventariada | Debe existir en tiendas.csv | Clave foránea |
| periodo | texto | Periodo mensual | AAAA-MM | Desde 2023-01 hasta 2025-12 |
| stock_inicial | entero | Stock inicial | 0 o mayor | Snapshot mensual |
| unidades_vendidas | entero | Unidades vendidas | 0 o mayor | Derivado de ventas.csv |
| reabastecimiento | entero | Unidades repuestas | 0 o mayor | Generado para cubrir demanda |
| stock_final | entero | Stock final | 0 o mayor | stock_inicial + reabastecimiento - unidades_vendidas |
| costo_almacenamiento_unitario | decimal | Costo unitario de almacenamiento | Positivo | Aumenta en Trujillo desde 2025-Q2 |
| costo_almacenamiento_total | decimal | Costo total de almacenamiento | Positivo | stock_final * costo_almacenamiento_unitario |

---

## Patrones sintéticos incorporados

1. Estacionalidad y campañas:
   - Campaña Escolar en febrero y marzo.
   - Día de la Madre en el segundo domingo de mayo, con ventana comercial.
   - Día del Padre en el tercer domingo de junio, con ventana comercial.
   - Fiestas Patrias en julio.
   - Cyber Wow en abril, julio y noviembre.
   - Black Friday en la última semana de noviembre.
   - Navidad en diciembre.

2. Relación campaña-categoría:
   - Cyber Wow favorece Tecnología y Cómputo, Electrohogar, Hogar, Moda y Calzado.
   - Campaña Escolar favorece Escolar y Oficina, Tecnología y Cómputo, Calzado y Moda.
   - Día de la Madre favorece Cuidado Personal, Moda, Calzado, Hogar y Electrohogar.
   - Día del Padre favorece Tecnología y Cómputo, Moda, Calzado, Electrohogar y Hogar.
   - Navidad favorece Juguetería, Tecnología y Cómputo, Electrohogar, Moda y Hogar.

3. Patrón diagnóstico:
   - Desde 2025-Q2, Trujillo presenta mayor descuento, menor margen y mayor costo de almacenamiento.

4. Churn:
   - Cliente inactivo si no compró en los últimos 90 días respecto al 2025-12-31.
   - El churn aumenta en clientes con baja frecuencia histórica.

5. Demanda predecible:
   - La cantidad vendida depende de categoría, subcategoría, mes, canal, ciudad, campaña, tipo de campaña y descuento.

6. Calidad de datos:
   - Faltantes controlados entre 1% y 3%.
   - Outliers controlados en cantidad y montos.
