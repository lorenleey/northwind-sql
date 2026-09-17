# Resolución de consultas — Northwind

## Pregunta 1 — [Título de la pregunta]

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


