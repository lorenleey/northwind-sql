# Resolución de consultas — Northwind

## Pregunta 1 —  Catálogo comercial activo

**Enunciado:** Obtén los productos que no están descatalogados y cuyo precio unitario esté entre 10 y 50 euros, ambos incluidos. Muestra el nombre del producto y su precio redondeado a dos decimales, ordenado de mayor a menor precio.

**Consulta:**

```sql
-- Productos no estás descontinuados cuyo precio está entre 10  y 50 ordenados de mayor a menor precio
SELECT product_name AS producto, 
ROUND((unit_price::numeric), 2) AS precio
FROM products
WHERE discontinued =0 
AND unit_price BETWEEN 10 AND 50
ORDER BY precio DESC;
```

**Resultado:**

![Resultado pregunta 1](img/p01.png)

**Comentario:** Se ha usado ROUND() porque es lo que se ha solicitado con los numéricos que representan dinero; además de eso en la condición se utiliza el nombre de la columna original pero a la hora de ordenar se usa el alias creado para la columna porque la consulta ya está hecha y la columna renombrada. 

## Pregunta 2 —  Concentración geográfica de la cartera

**Enunciado:** Cuenta cuántos clientes hay en cada país y muestra únicamente aquellos países con 5 o más clientes, ordenados de mayor a menor. Indica también cuántas ciudades distintas hay en cada uno de esos países.

**Consulta:**

```sql
-- Número de clientes en cada país, incluido cuantas ciudades hay de cada país ordenado de mayor número de clientes a menos
SELECT 
	country AS pais,
	COUNT(*) AS num_clientes,
	COUNT(DISTINCT city) AS num_ciudades
FROM customers
GROUP BY country
HAVING COUNT(*) >= 5
ORDER BY num_clientes DESC;
```

**Resultado:**

![Resultado pregunta 2](img/p02.png)

**Comentario:** Se utiliza HAVING() al tener un GROUP BY porque el filtro pasa por los grupos creados, uno por cada pais. Adicional a eso, se usa el COUNT(DISCTINCT...) porque no se desea contar todas las ciudades en cada país de cada cliente, sino el número de ciudades activas (con clientes) en cada país.

## Pregunta 3 —  Alerta de reposición

**Enunciado:** Localiza los productos activos cuyas unidades en stock sean inferiores o iguales a su nivel de reposición. Muestra el nombre, las unidades en stock, el nivel de reposición, las unidades ya pedidas al proveedor y una columna de texto que indique 'CRÍTICO' cuando el stock sea 0 y 'AVISO' en el resto de casos.

**Consulta:**

```sql
-- Productos activos cuyas unidades de stock sean iguales o inferior a la reposición
SELECT
	product_name AS producto,
	units_in_stock AS stock,
	reorder_level AS nivel_reposición, 
	units_on_order AS pedido_a_proveedor, 
	CASE units_in_stock
	WHEN 0 THEN 'CRÍTICO'
	ELSE 'AVISO' 
	END AS situacion
FROM products
WHERE discontinued =0
AND units_in_stock IS NOT NULL
AND units_in_stock >= reorder_level;
```

**Resultado:**

![Resultado pregunta 3](img/p03.png)

**Comentario:** Se tomo en cuenta al consultar cuales columnas aceptan NULL o no, y así se determinó que otro filtro a considerar era donde el stock no estuviera en NULL y así contar con los que SI tuvieran contenido en dicha columna. Se destaca además el uso de CASE WHEN en la columna situación, donde según el stock advertía con 'CRÍTICO' o 'AVISO'. 

## Pregunta 4 — Ficha completa de producto

**Enunciado:** Para los productos suministrados por empresas de Italia, Francia o España, muestra el nombre del producto, el nombre de la categoría, el nombre del proveedor, su país y su ciudad. Ordena por país y, dentro de cada país, por nombre de producto.

**Consulta:**

```sql
--Cada producto con su categoria y datos de contacto del proveedor

```

**Resultado:**

![Resultado pregunta 4](img/p04.png)

**Comentario:** 

## Pregunta 5 — Detalle valorizado de un pedido

**Enunciado:** Muestra, para ese pedido, el nombre del producto, el precio unitario aplicado, la cantidad, el descuento y el importe final de cada línea. Añade el nombre del cliente y la fecha del pedido.

**Consulta:**

```sql
-- Número de clientes en cada país, incluido cuantas ciudades hay de cada país ordenado de mayor número de clientes a menos

```

**Resultado:**

![Resultado pregunta 5](img/p05.png)

**Comentario:** Se utiliza HAVING() al tener un GROUP BY porque el filtro pasa por los grupos creados, uno por cada pais. Adicional a eso, se usa el COUNT(DISCTINCT...) porque no se desea contar todas las ciudades en cada país de cada cliente, sino el número de ciudades activas (con clientes) en cada país.

