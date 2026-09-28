# outer-joins-ministore
Ejercicio Modulo 5 Data Analytics COderhouse



 Preguntas de Negocio y Análisis Técnico

1. ¿Por qué usamos LEFT JOIN para la Consulta 1 y no INNER JOIN? ¿Qué habríamos perdido?
Usamos LEFT JOIN porque nuestra prioridad era revisar la lista completa de productos del catálogo, sin importar si tenían ventas o no.
Si hubiéramos usado un INNER JOIN, el sistema habría descartado automáticamente los productos que no registran ventas. Nos habríamos quedado "a ciegas" respecto al stock inmovilizado, creyendo erróneamente que todos los productos del catálogo se están vendiendo.

2. ¿Por qué usamos RIGHT JOIN para la Consulta 2? ¿Cómo se organizan las tablas?
Elegimos RIGHT JOIN para enfocar la consulta en la tabla de ventas (que se encuentra a la derecha del JOIN), mientras que la tabla de productos quedó a la izquierda.
Al hacerlo de esta forma, le pedimos al motor de base de datos que nos muestre todas las transacciones registradas, permitiéndonos detectar si existía alguna venta registrada de un producto que ya no existe (o nunca existió) en el catálogo.

3. ¿Qué significan los valores NULL en cada resultado?
En SQL, un valor NULL no representa un error en la consulta; al contrario, es una señal que nos da información clave sobre la falta de coincidencias:
En la Consulta 1 (venta_id es NULL): Significa que el producto existe en nuestro inventario pero nunca ha sido comprado por un cliente. (Ejemplo: Los productos "Hub USB-C" y "Parlante" aparecen en el catálogo, pero su ID de venta es NULL porque nadie los ha adquirido aún).
En la Consulta 2 (producto_id de productos es NULL): Significa que se registró una venta con un ID de producto que no coincide con ningún artículo del catálogo. (Ejemplo: La venta #10 fue registrada con el producto_id = 999, pero ese código no existe en la lista de productos).

4. ¿Cuándo usarías un FULL OUTER JOIN en un caso real de negocio?
Un FULL OUTER JOIN es la herramienta ideal cuando necesitas hacer una auditoría integral y comparar dos fuentes de datos sin perder ningún registro de ninguno de los dos lados.
Un caso típico en el mundo real es conciliar la información de dos departamentos o sistemas diferentes; por ejemplo, cruzar la base de datos de envíos de la empresa de logística contra los cobros registrados en la pasarela de pagos. De esta forma, puedes ver rápidamente en una sola tabla:
1. Envíos que sí fueron cobrados correctamente.
2. Cobros registrados que no tienen un envío asociado.
3. Envíos realizados que no han sido cobrados.
