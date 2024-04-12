# Taller Desarrollo de bases de datos (SQL)

## Creación de tablas e inserción de datos 

1. Creación tablas y la inserción de datos

   ```sql
   -- Crear tabla fabricante con código autoincrementable
   CREATE TABLE fabricante (
     codigo INT AUTO_INCREMENT PRIMARY KEY,
     nombre VARCHAR(100) NOT NULL
   );
   
   -- Insertar datos en la tabla fabricante
   INSERT INTO fabricante (nombre) VALUES
     ('Asus'),
     ('Lenovo'),
     ('Hewlett-Packard'),
     ('Seagate'),
     ('Crucial'),
     ('Gigabyte'),
     ('Huawei'),
     ('Xiaomi');
   
   -- Crear tabla producto con código autoincrementable
   CREATE TABLE producto (
     codigo INT AUTO_INCREMENT PRIMARY KEY,
     nombre VARCHAR(100) NOT NULL,
     precio DECIMAL(10,2) NOT NULL,
     fabricante_codigo INT NOT NULL,
     FOREIGN KEY (fabricante_codigo) REFERENCES fabricante(codigo)
   );
   
   -- Insertar datos en la tabla producto
   INSERT INTO producto (nombre, precio, fabricante_codigo) VALUES
     ('Disco duro SATA3 1TB', 86.99, 4),
     ('Disco SSD 1 TB', 150.99, 5),
     ('Monitor 24 LED Full HD', 202.00, 1),
     ('Portátil Yoga 520', 559.00, 2),
     ('Portátil Ideapd 3 ', 444.00, 2),
     ('Impresora HP Deskjet 3720', 59.99, 3),
     ('Impresora HP Laserjet Pro M26nw', 180.00, 3),
     ('Ratón óptico Logitech MX Epic', 53.99, 6),
     ('Teclado mecánico DUCKY Shine 7', 169.99, 6),
     ('Auriculares Bose Noise Cancelling 700', 379.00, 7),
     ('Webcam Logitech C920', 64.99, 6),
     ('Móvil Xiaomi Mi 9T', 360.00, 8),
     ('Móvil Huawei P30', 624.00, 7);
   ```

   

## Consultas sobre una tabla:

1. Lista el nombre de todos los productos que hay en la tabla producto:

```sql
SELECT nombre FROM producto;
```

2. Lista los nombres y los precios de todos los productos de la tabla producto:

```sql
SELECT nombre, precio FROM producto;
```

3. Lista todas las columnas de la tabla producto:

```sql
SELECT * FROM producto;
```

4. Lista el nombre de los productos, el precio en euros y el precio en dólares estadounidenses (USD):

```sql
SELECT nombre, precio, (precio * 1.05) AS dólares FROM producto;
```

5. Lista el nombre de los productos, el precio en euros y el precio en dólares estadounidenses (USD), utilizando los siguientes alias para las columnas: nombre de producto, euros, dólares:

```sql
SELECT nombre AS "nombre de producto", precio AS euros, (precio * 1.05) AS dólares FROM producto;
```

6. Lista los nombres y los precios de todos los productos de la tabla producto, convirtiendo los nombres a mayúscula:

```sql
SELECT UPPER(nombre), precio FROM producto;
```

7. Lista los nombres y los precios de todos los productos de la tabla producto, convirtiendo los nombres a minúscula:

```sql
SELECT LOWER(nombre), precio FROM producto;
```

8. Lista el nombre de todos los fabricantes en una columna, y en otra columna obtenga los dos primeros caracteres del nombre del fabricante en mayúsculas:

```sql
SELECT nombre, UPPER(SUBSTR(nombre, 1, 2)) AS abreviatura FROM fabricante;
```

9. Lista los nombres y los precios de todos los productos de la tabla producto, redondeando el valor del precio:

```sql
SELECT nombre, ROUND(precio) FROM producto;
```

10. Lista los nombres y los precios de todos los productos de la tabla producto, truncando el valor del precio para mostrarlo sin ninguna cifra decimal:

```sql
SELECT nombre, TRUNCATE(precio, 0) FROM producto;
```

11. Lista el identificador de los fabricantes que tienen productos en la tabla producto:

```sql
SELECT DISTINCT fabricante_id FROM producto;
```

12. Lista el identificador de los fabricantes que tienen productos en la tabla producto, eliminando los identificadores que aparecen repetidos:

```sql
SELECT DISTINCT fabricante_id FROM producto;
```

13. Lista los nombres de los fabricantes ordenados de forma ascendente:

```sql
SELECT nombre FROM fabricante ORDER BY nombre ASC;
```

14. Lista los nombres de los fabricantes ordenados de forma descendente:

```sql
SELECT nombre FROM fabricante ORDER BY nombre DESC;
```

15. Lista los nombres de los productos ordenados en primer lugar por el nombre de forma ascendente y en segundo lugar por el precio de forma descendente:

```sql
SELECT nombre FROM producto ORDER BY nombre ASC, precio DESC;
```

16. Devuelve una lista con las 5 primeras filas de la tabla fabricante:

```sql
SELECT * FROM fabricante LIMIT 5;
```

17. Devuelve una lista con 2 filas a partir de la cuarta fila de la tabla fabricante. La cuarta fila también se debe incluir en la respuesta:

```sql
SELECT * FROM fabricante LIMIT 3, 2;
```

18. Lista el nombre y el precio del producto más barato (Utilice solamente las cláusulas ORDER BY y LIMIT):

```sql
SELECT nombre, precio FROM producto ORDER BY precio ASC LIMIT 1;
```

19. Lista el nombre y el precio del producto más caro (Utilice solamente las cláusulas ORDER BY y LIMIT):

```sql
SELECT nombre, precio FROM producto ORDER BY precio DESC LIMIT 1;
```

20. Lista el nombre de todos los productos del fabricante cuyo identificador de fabricante es igual a 2:

```sql
SELECT nombre FROM producto WHERE fabricante_id = 2;
```

21. Lista el nombre de los productos que tienen un precio menor o igual a 120€:

```sql
SELECT nombre FROM producto WHERE precio <= 120;
```

22. Lista el nombre de los productos que tienen un precio mayor o igual a 400€:

```sql
SELECT nombre FROM producto WHERE precio >= 400;
```

23. Lista el nombre de los productos que no tienen un precio mayor o igual a 400€:

```sql
SELECT nombre FROM producto WHERE precio < 400;
```

24. Lista todos los productos que tengan un precio entre 80€ y 300€. Sin utilizar el operador BETWEEN:

```sql
SELECT nombre FROM producto WHERE precio >= 80 AND precio <= 300;
```

25. Lista todos los productos que tengan un precio entre 60€ y 200€. Utilizando el operador BETWEEN:

```sql
SELECT nombre FROM producto WHERE precio BETWEEN 60 AND 200;
```

26. Lista todos los productos que tengan un precio mayor que 200€ y que el identificador de fabricante sea igual a 6:

```sql
SELECT nombre FROM producto WHERE precio > 200 AND fabricante_id = 6;
```

27. Lista todos los productos donde el identificador de fabricante sea 1, 3 o 5. Sin utilizar el operador IN:

```sql
SELECT nombre FROM producto WHERE fabricante_id = 1 OR fabricante_id = 3 OR fabricante_id = 5;
```

28. Lista todos los productos donde el identificador de fabricante sea 1, 3 o 5. Utilizando el operador IN:

```sql
SELECT nombre FROM producto WHERE fabricante_id IN (1, 3, 5);
```

29. Lista el nombre y el precio de los productos en céntimos (Habrá que multiplicar por 100 el valor del precio). Cree un alias para la columna que contiene el precio que se llame céntimos:

```sql
SELECT nombre, (precio * 100) AS céntimos FROM producto;
```

30. Lista los nombres de los fabricantes cuyo nombre empiece por la letra S:

```sql
SELECT nombre FROM fabricante WHERE nombre LIKE 'S%';
```

31. Lista los nombres de los fabricantes cuyo nombre termine por la vocal e:

```sql
SELECT nombre FROM fabricante WHERE nombre LIKE '%e';
```

32. Lista los nombres de los fabricantes cuyo nombre contenga el carácter w:

```sql
SELECT nombre FROM fabricante WHERE nombre LIKE '%w%';
```

33. Lista los nombres de los fabricantes cuyo nombre sea de 4 caracteres:

```sql
SELECT nombre FROM fabricante WHERE LENGTH(nombre) = 4;
```

34. Devuelve una lista con el nombre de todos los productos que contienen la cadena Portátil en el nombre:

```sql
SELECT nombre FROM producto WHERE nombre LIKE '%Portátil%';
```

35. Devuelve una lista con el nombre de todos los productos que contienen la cadena Monitor en el nombre y tienen un precio inferior a 215 €:

```sql
SELECT nombre FROM producto WHERE nombre LIKE '%Monitor%' AND precio < 215;
```

36. Lista el nombre y el precio de todos los productos que tengan un precio mayor o igual a 180€. Ordene el resultado en primer lugar por el precio (en orden descendente) y en segundo lugar por el nombre (en orden ascendente):

```sql
SELECT nombre, precio FROM producto 
WHERE precio >= 180
ORDER BY precio DESC, nombre ASC;
```

Consultas multitabla (Composición interna):

1. Devuelve una lista con el nombre del producto, precio y nombre de fabricante de todos los productos de la base de datos:

```sql
SELECT producto.nombre, producto.precio, fabricante.nombre
FROM producto
INNER JOIN fabricante ON producto.fabricante_id = fabricante.id;
```

2. Devuelve una lista con el nombre del producto, precio y nombre de fabricante de todos los productos de la base de datos. Ordene el resultado por el nombre del fabricante, por orden alfabético:

```sql
SELECT producto.nombre, producto.precio, fabricante.nombre
FROM producto
INNER JOIN fabricante ON producto.fabricante_id = fabricante.id
ORDER BY fabricante.nombre ASC;
```

3. Devuelve una lista con el identificador del producto, nombre del producto, identificador del fabricante y nombre del fabricante, de todos los productos de la base de datos:

```sql
SELECT producto.id, producto.nombre, fabricante.id, fabricante.nombre
FROM producto
INNER JOIN fabricante ON producto.fabricante_id = fabricante.id;
```

4. Devuelve el nombre del producto, su precio y el nombre de su fabricante, del producto más barato:

```sql
SELECT producto.nombre, producto.precio, fabricante.nombre
FROM producto
INNER JOIN fabricante ON producto.fabricante_id = fabricante.id
ORDER BY producto.precio ASC
LIMIT 1;
```

5. Devuelve el nombre del producto, su precio y el nombre de su fabricante, del producto más caro:

```sql
SELECT producto.nombre, producto.precio, fabricante.nombre
FROM producto
INNER JOIN fabricante ON producto.fabricante_id = fabricante.id
ORDER BY producto.precio DESC
LIMIT 1;
```

6. Devuelve una lista de todos los productos del fabricante Lenovo:

```sql
SELECT producto.nombre
FROM producto
INNER JOIN fabricante ON producto.fabricante_id = fabricante.id
WHERE fabricante.nombre = 'Lenovo';
```

7. Devuelve una lista de todos los productos del fabricante Crucial que tengan un precio mayor que 200€:

```sql
SELECT producto.nombre
FROM producto
INNER JOIN fabricante ON producto.fabricante_id = fabricante.id
WHERE fabricante.nombre = 'Crucial' AND producto.precio > 200;
```

8. Devuelve un listado con todos los productos de los fabricantes Asus, Hewlett-Packardy Seagate. Sin utilizar el operador IN:

```sql
SELECT producto.nombre
FROM producto
INNER JOIN fabricante ON producto.fabricante_id = fabricante.id
WHERE fabricante.nombre = 'Asus' 
   OR fabricante.nombre = 'Hewlett-Packard'
   OR fabricante.nombre = 'Seagate';
```

9. Devuelve un listado con todos los productos de los fabricantes Asus, Hewlett-Packardy Seagate. Utilizando el operador IN:

```sql
SELECT producto.nombre
FROM producto
INNER JOIN fabricante ON producto.fabricante_id = fabricante.id
WHERE fabricante.nombre IN ('Asus', 'Hewlett-Packard', 'Seagate');
```

10. Devuelve un listado con el nombre y el precio de todos los productos de los fabricantes cuyo nombre termine por la vocal e:

```sql
SELECT producto.nombre, producto.precio
FROM producto
INNER JOIN fabricante ON producto.fabricante_id = fabricante.id
WHERE fabricante.nombre LIKE '%e';
```

11. Devuelve un listado con el nombre y el precio de todos los productos cuyo nombre de fabricante contenga el carácter w en su nombre:

```sql
SELECT producto.nombre, producto.precio
FROM producto
INNER JOIN fabricante ON producto.fabricante_id = fabricante.id
WHERE fabricante.nombre LIKE '%w%';
```

12. Devuelve un listado con el nombre de producto, precio y nombre de fabricante, de todos los productos que tengan un precio mayor o igual a 180€. Ordene el resultado en primer lugar por el precio (en orden descendente) y en segundo lugar por el nombre (en orden ascendente):

```sql
SELECT producto.nombre, producto.precio, fabricante.nombre
FROM producto
INNER JOIN fabricante ON producto.fabricante_id = fabricante.id
WHERE producto.precio >= 180
ORDER BY producto.precio DESC, producto.nombre ASC;
```

13. Devuelve un listado con el identificador y el nombre de fabricante, solamente de aquellos fabricantes que tienen productos asociados en la base de datos:

```sql
SELECT fabricante.id, fabricante.nombre
FROM fabricante
INNER JOIN producto ON fabricante.id = producto.fabricante_id
GROUP BY fabricante.id;
```
