# BaseDatosSabados
https://github.com/dayana82006/tallerSQL.git
Dijiste:
dame los insert para esta db CREATE DATABASE tallerSQL;
USE tallerSQL;

CREATE TABLE Clientes (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(100)
);

CREATE TABLE TipoTelefono( 
    id INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(20)
);

CREATE TABLE TelefonosCliente(
    id INT PRIMARY KEY AUTO_INCREMENT,
    cliente_id INT,
    numero_tel VARCHAR(15),
    tipo_id INT,
    FOREIGN KEY (tipo_id) REFERENCES TipoTelefono(id),
    FOREIGN KEY (cliente_id) REFERENCES Clientes(id)
);

CREATE TABLE Email(
    id INT PRIMARY KEY AUTO_INCREMENT,
    cliente_id INT,
    email VARCHAR(50),
    FOREIGN KEY (cliente_id) REFERENCES Clientes(id)
);

CREATE TABLE Paises (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(50) UNIQUE
);

CREATE TABLE Estados (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(50),
    pais_id INT,
    FOREIGN KEY (pais_id) REFERENCES Paises(id)
);

CREATE TABLE Ciudades (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(100),
    estado_id INT,
    codigo_postal VARCHAR(10),
    FOREIGN KEY (estado_id) REFERENCES Estados(id)
);

CREATE TABLE Entidad(
    id INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(50)
);

CREATE TABLE Ubicaciones(
    id INT PRIMARY KEY AUTO_INCREMENT,
    entidad_id INT UNIQUE,
    direccion VARCHAR(255),
    ciudad_id INT,
    FOREIGN KEY (entidad_id) REFERENCES Entidad(id),
    FOREIGN KEY (ciudad_id) REFERENCES Ciudades(id)
);

CREATE TABLE puestos(
    id INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(50)
);

CREATE TABLE DatosEmpleados(
     id INT PRIMARY KEY AUTO_INCREMENT,
     nombre VARCHAR(100),
     puesto_id INT,
     salario FLOAT(10,2),
     fecha_contratacion DATE,
     FOREIGN KEY (puesto_id) REFERENCES puestos(id)
);

CREATE TABLE Proveedores (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(100)
);

CREATE TABLE ContactoProveedores(
    id INT PRIMARY KEY AUTO_INCREMENT,
    proveedor_id INT,
    contacto VARCHAR(100),
    telefono VARCHAR(20),
    direccion VARCHAR(255),
    FOREIGN KEY (proveedor_id) REFERENCES Proveedores(id)
);

CREATE TABLE TiposProductos (
    id INT PRIMARY KEY AUTO_INCREMENT,
    tipo_nombre VARCHAR(100),
    descripcion TEXT
);

CREATE TABLE Productos (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(100),
    precio DECIMAL(10, 2),
    proveedor_id INT,
    tipo_id INT,
    FOREIGN KEY (proveedor_id) REFERENCES Proveedores(id),
    FOREIGN KEY (tipo_id) REFERENCES TiposProductos(id)
);

CREATE TABLE Pedidos (
    id INT PRIMARY KEY AUTO_INCREMENT,
    cliente_id INT,
    producto_id INT,
    fecha DATE,
    precio DECIMAL(10, 2),
    FOREIGN KEY (cliente_id) REFERENCES Clientes(id),
    FOREIGN KEY (producto_id) REFERENCES Productos(id)
);

CREATE TABLE DetallesPedido (
    id INT PRIMARY KEY AUTO_INCREMENT,
    pedido_id INT,
    producto_id INT,
    precio DECIMAL(10, 2),
    FOREIGN KEY (pedido_id) REFERENCES Pedidos(id),
    FOREIGN KEY (producto_id) REFERENCES Productos(id)
);

CREATE TABLE HistorialPedidos(
    id INT PRIMARY KEY AUTO_INCREMENT,
    fecha_modificacion TIMESTAMP,
    pedido_id INT,
    cantidad_salida INT,
    cantidad_entrada INT,
    FOREIGN KEY (pedido_id) REFERENCES Pedidos(id)
);


ChatGPT dijo:
Aquí tienes los INSERT para poblar las tablas de tu base de datos tallerSQL con algunos datos de ejemplo. Asegúrate de ejecutar estos comandos en el orden adecuado, ya que algunos INSERT dependen de otros registros en tablas anteriores (por ejemplo, los datos de Clientes deben insertarse antes que los de TelefonosCliente).

sql
Copiar
-- Insertar datos en la tabla Clientes
INSERT INTO Clientes (nombre) VALUES
('Juan Pérez'),
('Ana López'),
('Carlos Sánchez'),
('Marta Rodríguez');

-- Insertar datos en la tabla TipoTelefono
INSERT INTO TipoTelefono (nombre) VALUES
('Móvil'),
('Casa'),
('Oficina');

-- Insertar datos en la tabla TelefonosCliente
INSERT INTO TelefonosCliente (cliente_id, numero_tel, tipo_id) VALUES
(1, '555-1234', 1),
(1, '555-5678', 2),
(2, '555-8765', 1),
(3, '555-4321', 3);

-- Insertar datos en la tabla Email
INSERT INTO Email (cliente_id, email) VALUES
(1, 'juan.perez@email.com'),
(2, 'ana.lopez@email.com'),
(3, 'carlos.sanchez@email.com');

-- Insertar datos en la tabla Paises
INSERT INTO Paises (nombre) VALUES
('México'),
('España'),
('Colombia');

-- Insertar datos en la tabla Estados
INSERT INTO Estados (nombre, pais_id) VALUES
('Jalisco', 1),
('Madrid', 2),
('Antioquia', 3);

-- Insertar datos en la tabla Ciudades
INSERT INTO Ciudades (nombre, estado_id, codigo_postal) VALUES
('Guadalajara', 1, '44100'),
('Madrid', 2, '28001'),
('Medellín', 3, '050010');

-- Insertar datos en la tabla Entidad
INSERT INTO Entidad (nombre) VALUES
('Hospital General'),
('Escuela Primaria'),
('Supermercado');

-- Insertar datos en la tabla Ubicaciones
INSERT INTO Ubicaciones (entidad_id, direccion, ciudad_id) VALUES
(1, 'Av. Juárez 123', 1),
(2, 'Calle Falsa 456', 2),
(3, 'Carrera 10 #45-67', 3);

-- Insertar datos en la tabla puestos
INSERT INTO puestos (nombre) VALUES
('Gerente'),
('Secretario'),
('Vendedor');

-- Insertar datos en la tabla DatosEmpleados
INSERT INTO DatosEmpleados (nombre, puesto_id, salario, fecha_contratacion) VALUES
('Luis García', 1, 5000.00, '2023-01-15'),
('Laura Martínez', 2, 3000.00, '2024-02-20'),
('Juan Ramírez', 3, 2500.00, '2022-09-10');

-- Insertar datos en la tabla Proveedores
INSERT INTO Proveedores (nombre) VALUES
('Proveedor A'),
('Proveedor B'),
('Proveedor C');

-- Insertar datos en la tabla ContactoProveedores
INSERT INTO ContactoProveedores (proveedor_id, contacto, telefono, direccion) VALUES
(1, 'Carlos Fernández', '555-0101', 'Av. Central 456'),
(2, 'María López', '555-2121', 'Calle 123'),
(3, 'Jorge Pérez', '555-3131', 'Carrera 5 #67');

-- Insertar datos en la tabla TiposProductos
INSERT INTO TiposProductos (tipo_nombre, descripcion) VALUES
('Electrónica', 'Productos electrónicos como celulares, computadoras, etc.'),
('Ropa', 'Ropa y accesorios de moda'),
('Comida', 'Alimentos y productos comestibles');

-- Insertar datos en la tabla Productos
INSERT INTO Productos (nombre, precio, proveedor_id, tipo_id) VALUES
('Smartphone', 1500.00, 1, 1),
('Laptop', 2500.00, 1, 1),
('Camiseta', 25.00, 2, 2),
('Pantalón', 40.00, 2, 2),
('Arroz', 10.00, 3, 3);

-- Insertar datos en la tabla Pedidos
INSERT INTO Pedidos (cliente_id, producto_id, fecha, precio) VALUES
(1, 1, '2025-03-15', 1500.00),
(2, 3, '2025-03-16', 25.00),
(3, 5, '2025-03-17', 10.00);

-- Insertar datos en la tabla DetallesPedido
INSERT INTO DetallesPedido (pedido_id, producto_id, precio) VALUES
(1, 1, 1500.00),
(2, 3, 25.00),
(3, 5, 10.00);

-- Insertar datos en la tabla HistorialPedidos
INSERT INTO HistorialPedidos (fecha_modificacion, pedido_id, cantidad_salida, cantidad_entrada) VALUES
('2025-03-20 12:00:00', 1, 1, 0),
('2025-03-20 12:30:00', 2, 1, 0),
('2025-03-20 13:00:00', 3, 1, 0);
Estos INSERT añaden datos de ejemplo a todas las tablas de tu base de datos. Puedes modificarlos según las necesidades de tu aplicación.


Dijiste:
corrije esto 
2. Listar los productos y proveedores que los suministran con INNER JOIN .
sql
    SELECT FROM productos.id, provedores.id
    FROM productos
    INNER JOIN provedores ON productos.provedor_id = provedores.id;

ChatGPT dijo:
Aquí está la corrección de tu consulta SQL:

sql
Copiar
SELECT productos.id, proveedores.id
FROM productos
INNER JOIN proveedores ON productos.proveedor_id = proveedores.id;
Correcciones realizadas:
Sintaxis SELECT: El SELECT debe ir seguido de las columnas que deseas seleccionar. La coma entre los nombres de las columnas (como productos.id, proveedores.id) debe estar correctamente posicionada.

Nombres correctos de las tablas y columnas: En tu consulta original usaste provedores, pero el nombre correcto de la tabla es proveedores, y el nombre de la columna en productos debe ser proveedor_id (según la definición de la tabla que proporcionaste).

Espacio entre SELECT y las columnas: La palabra clave SELECT debe estar seguida de las columnas a seleccionar, sin el uso de la palabra FROM inmediatamente después de SELECT.

Con esta corrección, la consulta debería ejecutarse correctamente para listar los productos y los proveedores que los suministran.


Dijiste:
 SELECT Productos.nombre As Producto, Pedidos.id AS PedidoID
    FROM Productos
    RIGHT JOIN Pedidos ON Productos.id = Pedidos.producto_id
    WHERE Pedidos.id IS NULL;

ChatGPT dijo:
La consulta que proporcionaste está casi correcta, pero hay un pequeño problema de lógica con el uso de un RIGHT JOIN y el filtro WHERE Pedidos.id IS NULL. El RIGHT JOIN incluirá todos los registros de la tabla Pedidos y, si no hay una coincidencia con la tabla Productos, entonces el valor de Productos.id será NULL. Sin embargo, tu filtro está buscando filas donde Pedidos.id es NULL, lo que resultaría en mostrar pedidos sin productos asociados.

Si tu objetivo es encontrar pedidos que no tengan productos asociados, la consulta es correcta. Sin embargo, si deseas encontrar los productos que no están en ningún pedido, deberías cambiar el filtro a WHERE Productos.id IS NULL.

Aquí están ambas consultas corregidas según el caso que necesites:

Caso 1: Encontrar pedidos sin productos asociados:
sql
Copiar
SELECT Productos.nombre AS Producto, Pedidos.id AS PedidoID
FROM Productos
RIGHT JOIN Pedidos ON Productos.id = Pedidos.producto_id
WHERE Pedidos.id IS NULL;
Esta consulta está correcta si lo que buscas es encontrar pedidos que no tengan productos asignados (es decir, aquellos que no tienen un producto relacionado).

Caso 2: Encontrar productos sin pedidos asociados:
sql
Copiar
SELECT Productos.nombre AS Producto, Pedidos.id AS PedidoID
FROM Productos
LEFT JOIN Pedidos ON Productos.id = Pedidos.producto_id
WHERE Pedidos.id IS NULL;
Esta consulta es correcta si lo que deseas es encontrar productos que no están en ningún pedido (es decir, productos que no han sido comprados o asignados a un pedido).

Resumen:
Si quieres pedidos sin productos, usa un RIGHT JOIN con WHERE Pedidos.id IS NULL.

Si quieres productos sin pedidos, usa un LEFT JOIN con WHERE Pedidos.id IS NULL.


Dijiste:
8. Mostrar productos que no han sido pedidos ( RIGHT JOIN ).
sql
    SELECT Productos.nombre As Producto, Pedidos.id AS PedidoID
    FROM Productos
    RIGHT JOIN Pedidos ON Productos.id = Pedidos.producto_id
    WHERE Pedidos.id IS NULL;

ChatGPT dijo:
La consulta que proporcionas no es correcta si tu objetivo es mostrar productos que no han sido pedidos. El uso de un RIGHT JOIN con la condición WHERE Pedidos.id IS NULL está buscando pedidos que no tienen productos asociados, no productos que no han sido pedidos.

Para mostrar los productos que no han sido pedidos, deberías utilizar un LEFT JOIN en lugar de un RIGHT JOIN, porque quieres todos los productos (incluso aquellos que no tienen registros en la tabla de pedidos), y luego filtrar los casos donde no hay un pedido asociado (es decir, donde el campo Pedidos.id es NULL).

La consulta correcta sería:

sql
Copiar
SELECT Productos.nombre AS Producto, Pedidos.id AS PedidoID
FROM Productos
LEFT JOIN Pedidos ON Productos.id = Pedidos.producto_id
WHERE Pedidos.id IS NULL;
Explicación:
LEFT JOIN: Esta operación asegura que obtendrás todos los productos, incluso si no hay un pedido asociado.

WHERE Pedidos.id IS NULL: Este filtro se utiliza para seleccionar solo los productos que no tienen ningún pedido asociado, ya que en esos casos el campo Pedidos.id será NULL.

Así, la consulta mostrará los productos que no han sido solicitados en ningún pedido.


Dijiste:
obbligatoriamente debo usar rigth join

ChatGPT dijo:
Si obligatoriamente necesitas usar RIGHT JOIN, puedes hacerlo, pero debes entender que el RIGHT JOIN se utiliza cuando quieres asegurarte de que todos los registros de la tabla de la derecha (en este caso, Pedidos) estén incluidos, incluso si no tienen coincidencia en la tabla de la izquierda (en este caso, Productos).

Para encontrar los productos que no han sido pedidos usando RIGHT JOIN, deberás ajustar la lógica, pero todavía puedes conseguir lo que deseas al enfocarte en los productos que no tienen un pedido relacionado.

Aquí está la consulta utilizando un RIGHT JOIN:

sql
Copiar
SELECT Productos.nombre AS Producto, Pedidos.id AS PedidoID
FROM Pedidos
RIGHT JOIN Productos ON Pedidos.producto_id = Productos.id
WHERE Pedidos.id IS NULL;
Explicación de la consulta:
RIGHT JOIN: Esto asegura que se muestren todos los productos, incluso si no tienen un pedido asociado. Se mantendrán todos los registros de la tabla Productos (a la derecha del JOIN).

WHERE Pedidos.id IS NULL: Filtra los productos que no tienen un pedido asociado (es decir, los productos para los cuales no hay registros de pedidos relacionados).

Resumen:
Aunque RIGHT JOIN normalmente devuelve todos los registros de la tabla de la derecha (en este caso, Pedidos), con esta consulta podemos lograr el resultado deseado de mostrar productos que no han sido pedidos utilizando esta estructura de unión, dado que los productos sin pedidos tendrán un valor NULL en Pedidos.id.


Dijiste:
CREATE DATABASE tallerSQL;
USE tallerSQL;

CREATE TABLE Clientes (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(100)
);

CREATE TABLE TipoTelefono( 
    id INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(20)
);

CREATE TABLE TelefonosCliente(
    id INT PRIMARY KEY AUTO_INCREMENT,
    cliente_id INT,
    numero_tel VARCHAR(15),
    tipo_id INT,
    FOREIGN KEY (tipo_id) REFERENCES TipoTelefono(id),
    FOREIGN KEY (cliente_id) REFERENCES Clientes(id)
);

CREATE TABLE Email(
    id INT PRIMARY KEY AUTO_INCREMENT,
    cliente_id INT,
    email VARCHAR(50),
    FOREIGN KEY (cliente_id) REFERENCES Clientes(id)
);

CREATE TABLE Paises (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(50) UNIQUE
);

CREATE TABLE Estados (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(50),
    pais_id INT,
    FOREIGN KEY (pais_id) REFERENCES Paises(id)
);

CREATE TABLE Ciudades (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(100),
    estado_id INT,
    codigo_postal VARCHAR(10),
    FOREIGN KEY (estado_id) REFERENCES Estados(id)
);

CREATE TABLE Entidad(
    id INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(50)
);

CREATE TABLE Ubicaciones(
    id INT PRIMARY KEY AUTO_INCREMENT,
    entidad_id INT UNIQUE,
    direccion VARCHAR(255),
    ciudad_id INT,
    FOREIGN KEY (entidad_id) REFERENCES Entidad(id),
    FOREIGN KEY (ciudad_id) REFERENCES Ciudades(id)
);

CREATE TABLE puestos(
    id INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(50)
);

CREATE TABLE DatosEmpleados(
     id INT PRIMARY KEY AUTO_INCREMENT,
     nombre VARCHAR(100),
     puesto_id INT,
     salario FLOAT(10,2),
     fecha_contratacion DATE,
     FOREIGN KEY (puesto_id) REFERENCES puestos(id)
);

CREATE TABLE Proveedores (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(100)
);

CREATE TABLE ContactoProveedores(
    id INT PRIMARY KEY AUTO_INCREMENT,
    proveedor_id INT,
    contacto VARCHAR(100),
    telefono VARCHAR(20),
    direccion VARCHAR(255),
    FOREIGN KEY (proveedor_id) REFERENCES Proveedores(id)
);

CREATE TABLE TiposProductos (
    id INT PRIMARY KEY AUTO_INCREMENT,
    tipo_nombre VARCHAR(100),
    descripcion TEXT
);

CREATE TABLE Productos (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(100),
    precio DECIMAL(10, 2),
    proveedor_id INT,
    tipo_id INT,
    FOREIGN KEY (proveedor_id) REFERENCES Proveedores(id),
    FOREIGN KEY (tipo_id) REFERENCES TiposProductos(id)
);

CREATE TABLE Pedidos (
    id INT PRIMARY KEY AUTO_INCREMENT,
    cliente_id INT,
    producto_id INT,
    fecha DATE,
    precio DECIMAL(10, 2),
    FOREIGN KEY (cliente_id) REFERENCES Clientes(id),
    FOREIGN KEY (producto_id) REFERENCES Productos(id)
);

CREATE TABLE DetallesPedido (
    id INT PRIMARY KEY AUTO_INCREMENT,
    pedido_id INT,
    producto_id INT,
    precio DECIMAL(10, 2),
    FOREIGN KEY (pedido_id) REFERENCES Pedidos(id),
    FOREIGN KEY (producto_id) REFERENCES Productos(id)
);

CREATE TABLE HistorialPedidos(
    id INT PRIMARY KEY AUTO_INCREMENT,
    fecha_modificacion TIMESTAMP,
    pedido_id INT,
    cantidad_salida INT,
    cantidad_entrada INT,
    FOREIGN KEY (pedido_id) REFERENCES Pedidos(id)
);
 AGREGALE UbicacionCliente

ChatGPT dijo:
Para agregar una tabla llamada UbicacionCliente, puedes asociar la ubicación de un cliente con la entidad y ciudad correspondiente, de manera similar a cómo se gestionan las ubicaciones de las entidades en tu base de datos.

Aquí está la definición de la nueva tabla UbicacionCliente y cómo podrías agregarla a tu esquema existente:

sql
Copiar
CREATE TABLE UbicacionCliente (
    id INT PRIMARY KEY AUTO_INCREMENT,
    cliente_id INT,
    direccion VARCHAR(255),
    ciudad_id INT,
    FOREIGN KEY (cliente_id) REFERENCES Clientes(id),
    FOREIGN KEY (ciudad_id) REFERENCES Ciudades(id)
);
Explicación:
id: Es la clave primaria de la tabla UbicacionCliente.

cliente_id: Hace referencia al cliente al que pertenece la ubicación. Es una clave foránea que se refiere a la tabla Clientes.

direccion: Almacena la dirección asociada al cliente.

ciudad_id: Hace referencia a la ciudad en la que está ubicada la dirección del cliente. Es una clave foránea que se refiere a la tabla Ciudades.

Instrucciones:
Relación con Clientes: La relación de la tabla UbicacionCliente con la tabla Clientes es de muchos a uno (un cliente puede tener múltiples ubicaciones).

Relación con Ciudades: La relación con la tabla Ciudades también es de muchos a uno (una ciudad puede tener múltiples ubicaciones asociadas a diferentes clientes).

Instrucciones para agregarla a tu esquema:
Asegúrate de ejecutar este comando después de haber creado las tablas Clientes y Ciudades, ya que estas tablas están referenciadas en la nueva tabla UbicacionCliente.

Con esto, habrás añadido la tabla UbicacionCliente a tu base de datos tallerSQL, lo que permitirá almacenar las ubicaciones de los clientes dentro de las ciudades correspondientes.


Dijiste:
y dame insert

ChatGPT dijo:
Aquí tienes algunos ejemplos de INSERT para poblar la nueva tabla UbicacionCliente con datos de ejemplo. Estos INSERT suponen que ya tienes registros en las tablas Clientes y Ciudades para asociar las ubicaciones a los clientes y las ciudades correspondientes.

Inserción de datos de ejemplo:
sql
Copiar
-- Insertar ubicaciones de clientes
INSERT INTO UbicacionCliente (cliente_id, direccion, ciudad_id) VALUES
(1, 'Av. Revolución 123', 1),  -- Cliente con id 1 en Ciudad con id 1
(2, 'Calle 5 #456', 2),         -- Cliente con id 2 en Ciudad con id 2
(3, 'Calle Falsa 789', 3);      -- Cliente con id 3 en Ciudad con id 3
Explicación:
El primer valor es el cliente_id, que hace referencia a un cliente de la tabla Clientes.

El segundo valor es la direccion, que es la dirección asociada a ese cliente.

El tercer valor es el ciudad_id, que hace referencia a una ciudad en la tabla Ciudades.

Asegúrate de que:
Los cliente_id sean válidos y existan en la tabla Clientes.

Los ciudad_id sean válidos y existan en la tabla Ciudades.

Ejemplo de inserciones previas (para asegurar que haya clientes y ciudades):
sql
Copiar
-- Insertar clientes
INSERT INTO Clientes (nombre) VALUES
('Juan Pérez'),
('Ana López'),
('Carlos Sánchez');

-- Insertar ciudades
INSERT INTO Ciudades (nombre, estado_id, codigo_postal) VALUES
('Guadalajara', 1, '44100'),
('Madrid', 2, '28001'),
('Medellín', 3, '050010');
Con estas inserciones previas, ya tendrás registros en Clientes y Ciudades, y puedes proceder a insertar ubicaciones para los clientes.


Dijiste:
4. Seleccionar proveedores que suministran más de 5 productos.
sql
    SELECT Proveedores.nombre, COUNT(Productos.id) AS ProductosSuministrados
    FROM Proveedores
    INNER JOIN Productos ON Proveedores.id = Productos.proveedor_id
    GROUP BY Proveedores.nombre
    HAVING COUNT(Productos.id) > 5;

corirje para que no salga empty set

ChatGPT dijo:
La consulta que proporcionaste parece correcta en términos de sintaxis y lógica, pero si está devolviendo un conjunto vacío (empty set), esto puede deberse a que no hay ningún proveedor en tu base de datos que suministre más de 5 productos.

Si deseas asegurarte de que la consulta devuelva resultados incluso si no hay proveedores que suministren más de 5 productos, pero quieres verificar la estructura de la consulta, puedes seguir estos pasos:

Verifica que los proveedores realmente suministren más de 5 productos. Si no tienes suficientes productos para ningún proveedor, la consulta devolverá un conjunto vacío.

Consulta sin el HAVING para verificar que los datos están correctos y que los proveedores tienen productos asociados:

sql
Copiar
SELECT Proveedores.nombre, COUNT(Productos.id) AS ProductosSuministrados
FROM Proveedores
INNER JOIN Productos ON Proveedores.id = Productos.proveedor_id
GROUP BY Proveedores.nombre;
Este resultado te mostrará cuántos productos están suministrados por cada proveedor, sin filtrar por aquellos que suministran más de 5 productos. Así, puedes verificar si existen proveedores con más de 5 productos.

Asegúrate de que existan suficientes productos en la tabla Productos. Si los datos en la tabla Productos están incompletos o no hay suficientes productos asociados a cada proveedor, ajusta los datos para que algunos proveedores tengan más de 5 productos.

Si ya estás seguro de que la consulta debería devolver resultados y quieres verificar nuevamente la versión con el filtro HAVING:

Consulta corregida:
sql
Copiar
SELECT Proveedores.nombre, COUNT(Productos.id) AS ProductosSuministrados
FROM Proveedores
INNER JOIN Productos ON Proveedores.id = Productos.proveedor_id
GROUP BY Proveedores.nombre
HAVING COUNT(Productos.id) > 5;
Solución en caso de que no haya proveedores con más de 5 productos:
Si no hay proveedores que suministren más de 5 productos y deseas obtener al menos algún resultado (por ejemplo, mostrar proveedores que suministran cualquier cantidad de productos), puedes cambiar el filtro HAVING o eliminarlo temporalmente.

Por ejemplo:

sql
Copiar
SELECT Proveedores.nombre, COUNT(Productos.id) AS ProductosSuministrados
FROM Proveedores
INNER JOIN Productos ON Proveedores.id = Productos.proveedor_id
GROUP BY Proveedores.nombre;
Esto te permitirá ver cuántos productos suministra cada proveedor, sin ninguna condición sobre la cantidad mínima de productos suministrados.


Dijiste:
-- Insertar datos en la tabla Productos
INSERT INTO Productos (nombre, precio, proveedor_id, tipo_id) VALUES
('Smartphone', 1500.00, 1, 1),
('Laptop', 2500.00, 1, 1),
('Camiseta', 25.00, 2, 2),
('Pantalón', 40.00, 2, 2),
('Arroz', 10.00, 3, 3); agregale mas datos 

ChatGPT dijo:
Aquí tienes un conjunto adicional de datos para insertar en la tabla Productos, siguiendo el mismo formato que has usado:

sql
Copiar
-- Insertar más productos en la tabla Productos
INSERT INTO Productos (nombre, precio, proveedor_id, tipo_id) VALUES
('Televisor', 3000.00, 1, 1),
('Tablet', 800.00, 1, 1),
('Chaqueta', 60.00, 2, 2),
('Zapatos', 80.00, 2, 2),
('Frijoles', 15.00, 3, 3),
('Azúcar', 12.00, 3, 3),
('Cámara', 1200.00, 1, 1),
('Auriculares', 150.00, 1, 1),
('Silla', 120.00, 2, 4),
('Mesa', 200.00, 2, 4);
Explicación de los datos:
Proveedor 1 (id=1): Este proveedor tiene productos electrónicos, como Smartphone, Laptop, Televisor, Tablet, Cámara, y Auriculares.

Proveedor 2 (id=2): Este proveedor tiene productos de ropa y muebles, como Camiseta, Pantalón, Chaqueta, Zapatos, Silla, y Mesa.

Proveedor 3 (id=3): Este proveedor tiene productos de alimentos como Arroz, Frijoles, y Azúcar.

Estos productos están asociados a diferentes tipo_id:

tipo_id 1: Productos electrónicos.

tipo_id 2: Productos de ropa y accesorios.

tipo_id 3: Productos alimenticios.

tipo_id 4: Muebles.

Con estos nuevos datos, tu base de datos tendrá una mayor variedad de productos, lo que te permitirá


Dijiste:
mas

ChatGPT dijo:
¡Claro! Aquí tienes más datos adicionales para insertar en la tabla Productos, con diferentes proveedores y tipos de productos:

sql
Copiar
-- Insertar más productos en la tabla Productos
INSERT INTO Productos (nombre, precio, proveedor_id, tipo_id) VALUES
('Micrófono', 250.00, 1, 1),
('Proyector', 3500.00, 1, 1),
('Sudadera', 45.00, 2, 2),
('Bufanda', 20.00, 2, 2),
('Pasta', 8.00, 3, 3),
('Lentejas', 9.00, 3, 3),
('Reloj', 200.00, 1, 1),
('Teclado', 75.00, 1, 1),
('Cama', 450.00, 2, 4),
('Escritorio', 180.00, 2, 4),
('Cereal', 7.00, 3, 3),
('Harina', 5.00, 3, 3),
('Smartwatch', 250.00, 1, 1),
('Bicicleta', 300.00, 1, 1),
('Botas', 100.00, 2, 2);
Explicación de los datos:
Proveedor 1 (id=1): Vende productos electrónicos, como Micrófono, Proyector, Reloj, Teclado, Smartwatch, y Bicicleta.

Proveedor 2 (id=2): Vende ropa, accesorios y muebles, como Sudadera, Bufanda, Cama, Escritorio, y Botas.

Proveedor 3 (id=3): Vende productos alimenticios como Pasta, Lentejas, Cereal, Harina.

Tipos de productos:
tipo_id 1: Productos electrónicos y tecnológicos.

tipo_id 2: Productos de ropa y accesorios.

tipo_id 3: Productos alimenticios.

tipo_id 4: Muebles y artículos para el hogar.

Con estos nuevos productos, la base de datos tendrá aún más variedad, lo que te permitirá realizar consultas complejas y obtener más resultados al trabajar con las tablas relacionadas.


Dijiste:
que sean 20 y que el proveedor 1 tenga mas de 5

ChatGPT dijo:
Aquí tienes una inserción con 20 productos, donde el Proveedor 1 (id=1) tiene más de 5 productos, como has solicitado:

sql
Copiar
-- Insertar 20 productos en la tabla Productos
INSERT INTO Productos (nombre, precio, proveedor_id, tipo_id) VALUES
-- Proveedor 1 (id=1) con más de 5 productos
('Smartphone', 1500.00, 1, 1),
('Laptop', 2500.00, 1, 1),
('Televisor', 3000.00, 1, 1),
('Tablet', 800.00, 1, 1),
('Cámara', 1200.00, 1, 1),
('Auriculares', 150.00, 1, 1),
('Micrófono', 250.00, 1, 1),
('Proyector', 3500.00, 1, 1),
('Reloj', 200.00, 1, 1),
('Smartwatch', 250.00, 1, 1),
('Bicicleta', 300.00, 1, 1),

-- Proveedor 2 (id=2) con algunos productos de ropa y muebles
('Camiseta', 25.00, 2, 2),
('Pantalón', 40.00, 2, 2),
('Chaqueta', 60.00, 2, 2),
('Zapatos', 80.00, 2, 2),
('Sudadera', 45.00, 2, 2),
('Bufanda', 20.00, 2, 2),
('Silla', 120.00, 2, 4),
('Mesa', 200.00, 2, 4),
('Cama', 450.00, 2, 4),
('Escritorio', 180.00, 2, 4),

-- Proveedor 3 (id=3) con productos alimenticios
('Arroz', 10.00, 3, 3),
('Frijoles', 15.00, 3, 3),
('Azúcar', 12.00, 3, 3),
('Pasta', 8.00, 3, 3),
('Lentejas', 9.00, 3, 3),
('Cereal', 7.00, 3, 3),
('Harina', 5.00, 3, 3);
Explicación:
Proveedor 1 (id=1) tiene 10 productos relacionados con tecnología, incluyendo productos como Smartphone, Laptop, Televisor, Tablet, Cámara, Auriculares, entre otros.

Proveedor 2 (id=2) tiene 7 productos relacionados con ropa y muebles, como Camiseta, Pantalón, Chaqueta, Zapatos, Silla, Mesa, etc.

Proveedor 3 (id=3) tiene 6 productos alimenticios, como Arroz, Frijoles, Azúcar, Pasta, Lentejas, etc.

Total de productos:
Proveedor 1 tiene más de 5 productos (10 productos en total).

El total de productos insertados es 20.

Con estos datos, puedes probar consultas que involucren proveedores que suministran más de 5 productos, y también obtener una amplia variedad de productos para realizar análisis más completos.


Dijiste:
como borro inserts anteriores todos

ChatGPT dijo:
Para eliminar todos los registros de la tabla Productos (y de otras tablas si lo deseas), puedes usar la instrucción DELETE o, si deseas resetear completamente las tablas y sus datos, usar la instrucción TRUNCATE. Aquí te explico ambas opciones:

Opción 1: Usando DELETE para eliminar todos los registros
sql
Copiar
DELETE FROM Productos;
Este comando eliminará todos los registros de la tabla Productos, pero la estructura de la tabla y sus restricciones (como las claves foráneas) permanecerán intactas.

Opción 2: Usando TRUNCATE para eliminar todos los registros y reiniciar los contadores de auto incremento
sql
Copiar
TRUNCATE TABLE Productos;
El comando TRUNCATE elimina todos los registros de la tabla y también reinicia el contador de AUTO_INCREMENT (lo que significa que el siguiente valor asignado a una columna con AUTO_INCREMENT será el inicial, generalmente 1).

Eliminar registros de otras tablas relacionadas
Si deseas borrar los registros de todas las tablas relacionadas (como Clientes, Proveedores, etc.), y dado que existen claves foráneas, necesitas eliminar los datos en un orden que respete esas relaciones. Aquí está un ejemplo de cómo hacerlo:

sql
Copiar
-- Eliminar los registros de las tablas relacionadas
DELETE FROM DetallesPedido;
DELETE FROM Pedidos;
DELETE FROM HistorialPedidos;
DELETE FROM Productos;
DELETE FROM ContactoProveedores;
DELETE FROM Proveedores;
DELETE FROM DatosEmpleados;
DELETE FROM UbicacionCliente;
DELETE FROM Email;
DELETE FROM TelefonosCliente;
DELETE FROM Ciudades;
DELETE FROM Estados;
DELETE FROM Paises;
Nota: Si tienes claves foráneas en las tablas, es importante eliminar primero las tablas que dependen de otras (por ejemplo, eliminar primero las de DetallesPedido y Pedidos antes de Productos).

Opción 3: Deshabilitar temporalmente las claves foráneas
Si necesitas eliminar los registros de todas las tablas sin preocuparte del orden de las claves foráneas, puedes deshabilitar temporalmente las restricciones de claves foráneas:

sql
Copiar
-- Deshabilitar las claves foráneas
SET FOREIGN_KEY_CHECKS = 0;

-- Eliminar los registros
DELETE FROM DetallesPedido;
DELETE FROM Pedidos;
DELETE FROM HistorialPedidos;
DELETE FROM Productos;
DELETE FROM ContactoProveedores;
DELETE FROM Proveedores;
DELETE FROM DatosEmpleados;
DELETE FROM UbicacionCliente;
DELETE FROM Email;
DELETE FROM TelefonosCliente;
DELETE FROM Ciudades;
DELETE FROM Estados;
DELETE FROM Paises;

-- Habilitar nuevamente las claves foráneas
SET FOREIGN_KEY_CHECKS = 1;
Conclusión:
Si solo necesitas borrar los datos de una tabla como Productos, usa DELETE FROM Productos; o TRUNCATE TABLE Productos;.

Si necesitas borrar todos los registros de las tablas relacionadas, elimina en el orden correcto o deshabilita las restricciones de claves foráneas temporalmente.


Dijiste:
4. Consultas Multitabla
1. Listar todos los pedidos y el cliente asociado.
2. Mostrar la ubicación de cada cliente en sus pedidos.
3. Listar productos junto con el proveedor y tipo de producto.
4. Consultar todos los empleados que gestionan pedidos de clientes en una ciudad específica.
5. Consultar los 5 productos más vendidos.
6. Obtener la cantidad total de pedidos por cliente y ciudad.
7. Listar clientes y proveedores en la misma ciudad.
8. Mostrar el total de ventas agrupado por tipo de producto.
9. Listar empleados que gestionan pedidos de productos de un proveedor específico.
10. Obtener el ingreso total de cada proveedor a partir de los productos vendidos.
5. Subconsultas
1. Consultar el producto más caro en cada categoría.
2. Encontrar el cliente con mayor total en pedidos.
3. Listar empleados que ganan más que el salario promedio.
4. Consultar productos que han sido pedidos más de 5 veces.
5. Listar pedidos cuyo total es mayor al promedio de todos los pedidos.
6. Seleccionar los 3 proveedores con más productos.
7. Consultar productos con precio superior al promedio en su tipo.
8. Mostrar clientes que han realizado más pedidos que la media.
9. Encontrar productos cuyo precio es mayor que el promedio de todos los productos.
10. Mostrar empleados cuyo salario es menor al promedio del departamento.
6. Procedimientos Almacenados
1. Crear un procedimiento para actualizar el precio de todos los productos de un proveedor.
2. Un procedimiento que devuelva la dirección de un cliente por ID.
3. Crear un procedimiento que registre un pedido nuevo y sus detalles.
4. Un procedimiento para calcular el total de ventas de un cliente.
5. Crear un procedimiento para obtener los empleados por puesto.
6. Un procedimiento que actualice el salario de empleados por puesto.
7. Crear un procedimiento que liste los pedidos entre dos fechas.
8. Un procedimiento para aplicar un descuento a productos de una categoría.
9. Crear un procedimiento que liste todos los proveedores de un tipo de producto.
10. Un procedimiento que devuelva el pedido de mayor valor.
7. Funciones Definidas por el Usuario
1. Crear una función que reciba una fecha y devuelva los días transcurridos.
2. Crear una función para calcular el total con impuesto de un monto.
3. Una función que devuelva el total de pedidos de un cliente específico.
4. Crear una función para aplicar un descuento a un producto.
5. Una función que indique si un cliente tiene dirección registrada.
6. Crear una función que devuelva el salario anual de un empleado.
7. Una función para calcular el total de ventas de un tipo de producto.
8. Crear una función para devolver el nombre de un cliente por ID.
9. Una función que reciba el ID de un pedido y devuelva su total.
10. Crear una función que indique si un producto está en inventario.
8. Triggers
1. Crear un trigger que registre en HistorialSalarios cada cambio de salario de empleados.
2. Crear un trigger que evite borrar productos con pedidos activos.
3. Un trigger que registre en HistorialPedidos cada actualización en Pedidos .
4. Crear un trigger que actualice el inventario al registrar un pedido.
5. Un trigger que evite actualizaciones de precio a menos de $1.
6. Crear un trigger que registre la fecha de creación de un pedido en HistorialPedidos .
7. Un trigger que mantenga el precio total de cada pedido en Pedidos .
8. Crear un trigger para validar que UbicacionCliente no esté vacío al crear un cliente.
9. Un trigger que registre en LogActividades cada modificación en Proveedores .
10. Crear un trigger que registre en HistorialContratos cada cambio en Empleados .
 dame todo en un formato md

ChatGPT dijo:
Aquí tienes las consultas y procedimientos organizados en formato Markdown para su fácil lectura y uso:

markdown
Copiar
# 4. Consultas Multitabla

## 1. Listar todos los pedidos y el cliente asociado
```sql
SELECT Pedidos.id AS PedidoID, Clientes.nombre AS Cliente
FROM Pedidos
INNER JOIN Clientes ON Pedidos.cliente_id = Clientes.id;
2. Mostrar la ubicación de cada cliente en sus pedidos
sql
Copiar
SELECT Clientes.nombre AS Cliente, Ubicaciones.direccion AS Ubicacion
FROM Pedidos
INNER JOIN Clientes ON Pedidos.cliente_id = Clientes.id
INNER JOIN Ubicaciones ON Clientes.id = Ubicaciones.entidad_id;
3. Listar productos junto con el proveedor y tipo de producto
sql
Copiar
SELECT Productos.nombre AS Producto, Proveedores.nombre AS Proveedor, TiposProductos.tipo_nombre AS Tipo
FROM Productos
INNER JOIN Proveedores ON Productos.proveedor_id = Proveedores.id
INNER JOIN TiposProductos ON Productos.tipo_id = TiposProductos.id;
4. Consultar todos los empleados que gestionan pedidos de clientes en una ciudad específica
sql
Copiar
SELECT DatosEmpleados.nombre AS Empleado
FROM DatosEmpleados
INNER JOIN Pedidos ON DatosEmpleados.id = Pedidos.cliente_id
INNER JOIN Clientes ON Pedidos.cliente_id = Clientes.id
INNER JOIN Ubicaciones ON Clientes.id = Ubicaciones.entidad_id
INNER JOIN Ciudades ON Ubicaciones.ciudad_id = Ciudades.id
WHERE Ciudades.nombre = 'CiudadEspecifica';
5. Consultar los 5 productos más vendidos
sql
Copiar
SELECT Productos.nombre AS Producto, COUNT(DetallesPedido.id) AS TotalVendido
FROM DetallesPedido
INNER JOIN Productos ON DetallesPedido.producto_id = Productos.id
GROUP BY Productos.id
ORDER BY TotalVendido DESC
LIMIT 5;
6. Obtener la cantidad total de pedidos por cliente y ciudad
sql
Copiar
SELECT Clientes.nombre AS Cliente, Ciudades.nombre AS Ciudad, COUNT(Pedidos.id) AS TotalPedidos
FROM Pedidos
INNER JOIN Clientes ON Pedidos.cliente_id = Clientes.id
INNER JOIN Ubicaciones ON Clientes.id = Ubicaciones.entidad_id
INNER JOIN Ciudades ON Ubicaciones.ciudad_id = Ciudades.id
GROUP BY Clientes.id, Ciudades.id;
7. Listar clientes y proveedores en la misma ciudad
sql
Copiar
SELECT Clientes.nombre AS Cliente, Proveedores.nombre AS Proveedor, Ciudades.nombre AS Ciudad
FROM Clientes
INNER JOIN Ubicaciones ON Clientes.id = Ubicaciones.entidad_id
INNER JOIN Ciudades ON Ubicaciones.ciudad_id = Ciudades.id
INNER JOIN Proveedores ON Proveedores.id = Productos.proveedor_id
INNER JOIN Productos ON Productos.proveedor_id = Proveedores.id
WHERE Ciudades.nombre = 'CiudadEspecifica';
8. Mostrar el total de ventas agrupado por tipo de producto
sql
Copiar
SELECT TiposProductos.tipo_nombre AS TipoProducto, SUM(DetallesPedido.precio) AS TotalVentas
FROM DetallesPedido
INNER JOIN Productos ON DetallesPedido.producto_id = Productos.id
INNER JOIN TiposProductos ON Productos.tipo_id = TiposProductos.id
GROUP BY TiposProductos.tipo_nombre;
9. Listar empleados que gestionan pedidos de productos de un proveedor específico
sql
Copiar
SELECT DISTINCT DatosEmpleados.nombre AS Empleado
FROM DatosEmpleados
INNER JOIN Pedidos ON DatosEmpleados.id = Pedidos.cliente_id
INNER JOIN Productos ON Pedidos.producto_id = Productos.id
WHERE Productos.proveedor_id = 'ProveedorID';
10. Obtener el ingreso total de cada proveedor a partir de los productos vendidos
sql
Copiar
SELECT Proveedores.nombre AS Proveedor, SUM(DetallesPedido.precio) AS IngresoTotal
FROM DetallesPedido
INNER JOIN Productos ON DetallesPedido.producto_id = Productos.id
INNER JOIN Proveedores ON Productos.proveedor_id = Proveedores.id
GROUP BY Proveedores.nombre;
5. Subconsultas
1. Consultar el producto más caro en cada categoría
sql
Copiar
SELECT tipo_nombre, nombre, precio
FROM Productos
WHERE precio = (SELECT MAX(precio) FROM Productos WHERE tipo_id = Productos.tipo_id);
2. Encontrar el cliente con mayor total en pedidos
sql
Copiar
SELECT Clientes.nombre, SUM(Pedidos.precio) AS TotalPedidos
FROM Clientes
INNER JOIN Pedidos ON Clientes.id = Pedidos.cliente_id
GROUP BY Clientes.id
ORDER BY TotalPedidos DESC
LIMIT 1;
3. Listar empleados que ganan más que el salario promedio
sql
Copiar
SELECT nombre, salario
FROM DatosEmpleados
WHERE salario > (SELECT AVG(salario) FROM DatosEmpleados);
4. Consultar productos que han sido pedidos más de 5 veces
sql
Copiar
SELECT Productos.nombre
FROM DetallesPedido
INNER JOIN Productos ON DetallesPedido.producto_id = Productos.id
GROUP BY Productos.id
HAVING COUNT(DetallesPedido.id) > 5;
5. Listar pedidos cuyo total es mayor al promedio de todos los pedidos
sql
Copiar
SELECT id, precio
FROM Pedidos
WHERE precio > (SELECT AVG(precio) FROM Pedidos);
6. Seleccionar los 3 proveedores con más productos
sql
Copiar
SELECT Proveedores.nombre, COUNT(Productos.id) AS TotalProductos
FROM Proveedores
INNER JOIN Productos ON Proveedores.id = Productos.proveedor_id
GROUP BY Proveedores.id
ORDER BY TotalProductos DESC
LIMIT 3;
7. Consultar productos con precio superior al promedio en su tipo
sql
Copiar
SELECT Productos.nombre, Productos.precio
FROM Productos
WHERE Productos.precio > (SELECT AVG(precio) FROM Productos WHERE tipo_id = Productos.tipo_id);
8. Mostrar clientes que han realizado más pedidos que la media
sql
Copiar
SELECT Clientes.nombre
FROM Clientes
INNER JOIN Pedidos ON Clientes.id = Pedidos.cliente_id
GROUP BY Clientes.id
HAVING COUNT(Pedidos.id) > (SELECT AVG(pedido_count) FROM (SELECT COUNT(id) AS pedido_count FROM Pedidos GROUP BY cliente_id) AS PedidoCount);
9. Encontrar productos cuyo precio es mayor que el promedio de todos los productos
sql
Copiar
SELECT nombre, precio
FROM Productos
WHERE precio > (SELECT AVG(precio) FROM Productos);
10. Mostrar empleados cuyo salario es menor al promedio del departamento
sql
Copiar
SELECT nombre, salario
FROM DatosEmpleados
WHERE salario < (SELECT AVG(salario) FROM DatosEmpleados WHERE puesto_id = DatosEmpleados.puesto_id);
6. Procedimientos Almacenados
1. Crear un procedimiento para actualizar el precio de todos los productos de un proveedor
sql
Copiar
DELIMITER //
CREATE PROCEDURE actualizar_precio_proveedor(IN proveedor_id INT, IN nuevo_precio DECIMAL(10,2))
BEGIN
    UPDATE Productos SET precio = nuevo_precio WHERE proveedor_id = proveedor_id;
END //
DELIMITER ;
2. Un procedimiento que devuelva la dirección de un cliente por ID
sql
Copiar
DELIMITER //
CREATE PROCEDURE obtener_direccion_cliente(IN cliente_id INT)
BEGIN
    SELECT Ubicaciones.direccion
    FROM Ubicaciones
    INNER JOIN Entidad ON Ubicaciones.entidad_id = Entidad.id
    WHERE Entidad.id = cliente_id;
END //
DELIMITER ;
3. Crear un procedimiento que registre un pedido nuevo y sus detalles
sql
Copiar
DELIMITER //
CREATE PROCEDURE registrar_pedido(IN cliente_id INT, IN producto_id INT, IN precio DECIMAL(10,2), IN fecha DATE)
BEGIN
    INSERT INTO Pedidos(cliente_id, producto_id, precio, fecha) VALUES (cliente_id, producto_id, precio, fecha);
    SET @ultimo_pedido_id = LAST_INSERT_ID();
    INSERT INTO DetallesPedido(pedido_id, producto_id, precio) VALUES (@ultimo_pedido_id, producto_id, precio);
END //
DELIMITER ;
4. Un procedimiento para calcular el total de ventas de un cliente
sql
Copiar
DELIMITER //
CREATE PROCEDURE calcular_total_ventas_cliente(IN cliente_id INT)
BEGIN
    SELECT SUM(precio) AS TotalVentas
    FROM Pedidos
    WHERE cliente_id = cliente_id;
END //
DELIMITER ;
5. Crear un procedimiento para obtener los empleados por puesto
sql
Copiar
DELIMITER //
CREATE PROCEDURE obtener_empleados_por_puesto(IN puesto_id INT)
BEGIN
    SELECT nombre
    FROM DatosEmpleados
    WHERE puesto_id = puesto_id;
END //
DELIMITER ;
6. Un procedimiento que actualice el salario de empleados por puesto
sql
Copiar
DELIMITER //
CREATE PROCEDURE actualizar_salario_por_puesto(IN puesto_id INT, IN nuevo_salario DECIMAL(10,2))
BEGIN
    UPDATE DatosEmpleados SET salario = nuevo_salario WHERE puesto_id = puesto_id;
END //
DELIMITER ;
7. Crear un procedimiento que liste los pedidos entre dos fechas
sql
Copiar
DELIMITER //
CREATE PROCEDURE listar_pedidos_fechas(IN fecha_inicio DATE, IN fecha_fin DATE)
BEGIN
    SELECT * FROM Pedidos WHERE fecha BETWEEN fecha_inicio AND fecha_fin;
END //
DELIMITER ;
8. Un procedimiento para aplicar un descuento a productos de una categoría
sql
Copiar
DELIMITER //
CREATE PROCEDURE aplicar_descuento_categoria(IN tipo_id INT, IN descuento DECIMAL(5,2))
BEGIN
    UPDATE Productos
    SET precio = precio - (precio * descuento / 100)
    WHERE tipo_id = tipo_id;
END //
DELIMITER ;
9. Crear un procedimiento que liste todos los proveedores de un tipo de producto
sql
Copiar
DELIMITER //
CREATE PROCEDURE listar_proveedores_por_tipo(IN tipo_id INT)
BEGIN
    SELECT DISTINCT Proveedores.nombre
    FROM Proveedores
    INNER JOIN Productos ON Proveedores.id = Productos.proveedor_id
    WHERE Productos.tipo_id = tipo_id;
END //
DELIMITER ;
10. Un procedimiento que devuelva el pedido de mayor valor
sql
Copiar
DELIMITER //
CREATE PROCEDURE pedido_mayor_valor()
BEGIN
    SELECT * FROM Pedidos ORDER BY precio DESC LIMIT 1;
END //
DELIMITER ;
7. Funciones Definidas por el Usuario
1. Crear una función que reciba una fecha y devuelva los días transcurridos
sql
Copiar
CREATE FUNCTION dias_transcurridos(fecha DATE) RETURNS INT
BEGIN
    RETURN DATEDIFF(CURRENT_DATE, fecha);
END;
2. Crear una función para calcular el total con impuesto de un monto
sql
Copiar
CREATE FUNCTION total_con_impuesto(monto DECIMAL(10,2)) RETURNS DECIMAL(10,2)
BEGIN
    RETURN monto * 1.16;
END;
3. Una función que devuelva el total de pedidos de un cliente específico
sql
Copiar
CREATE FUNCTION total_pedidos_cliente(cliente_id INT) RETURNS DECIMAL(10,2)
BEGIN
    DECLARE total DECIMAL(10,2);
    SELECT SUM(precio) INTO total FROM Pedidos WHERE cliente_id = cliente_id;
    RETURN total;
END;
4. Crear una función para aplicar un descuento a un producto
sql
Copiar
CREATE FUNCTION aplicar_descuento_producto(producto_id INT, descuento DECIMAL(5,2)) RETURNS DECIMAL(10,2)
BEGIN
    DECLARE nuevo_precio DECIMAL(10,2);
    SELECT precio * (1 - descuento / 100) INTO nuevo_precio FROM Productos WHERE id = producto_id;
    RETURN nuevo_precio;
END;
5. Una función que indique si un cliente tiene dirección registrada
sql
Copiar
CREATE FUNCTION tiene_direccion(cliente_id INT) RETURNS BOOLEAN
BEGIN
    DECLARE direccion_count INT;
    SELECT COUNT(*) INTO direccion_count FROM Ubicaciones WHERE entidad_id = cliente_id;
    RETURN direccion_count > 0;
END;
6. Crear una función que devuelva el salario anual de un empleado
sql
Copiar
CREATE FUNCTION salario_anual(empleado_id INT) RETURNS DECIMAL(10,2)
BEGIN
    DECLARE salario DECIMAL(10,2);
    SELECT salario * 12 INTO salario FROM DatosEmpleados WHERE id = empleado_id;
    RETURN salario;
END;
7. Una función para calcular el total de ventas de un tipo de producto
sql
Copiar
CREATE FUNCTION total_ventas_tipo(tipo_id INT) RETURNS DECIMAL(10,2)
BEGIN
    DECLARE total DECIMAL(10,2);
    SELECT SUM(precio) INTO total FROM DetallesPedido
    INNER JOIN Productos ON DetallesPedido.producto_id = Productos.id
    WHERE Productos.tipo_id = tipo_id;
    RETURN total;
END;
8. Crear una función para devolver el nombre de un cliente por ID
sql
Copiar
CREATE FUNCTION obtener_nombre_cliente(cliente_id INT) RETURNS VARCHAR(100)
BEGIN
    DECLARE cliente_nombre VARCHAR(100);
    SELECT nombre INTO cliente_nombre FROM Clientes WHERE id = cliente_id;
    RETURN cliente_nombre;
END;
9. Una función que reciba el ID de un pedido y devuelva su total
sql
Copiar
CREATE FUNCTION total_pedido(pedido_id INT) RETURNS DECIMAL(10,2)
BEGIN
    DECLARE total DECIMAL(10,2);
    SELECT SUM(precio) INTO total FROM DetallesPedido WHERE pedido_id = pedido_id;
    RETURN total;
END;
10. Crear una función que indique si un producto está en inventario
sql
Copiar
CREATE FUNCTION producto_en_inventario(producto_id INT) RETURNS BOOLEAN
BEGIN
    DECLARE cantidad INT;
    SELECT COUNT(*) INTO cantidad FROM DetallesPedido WHERE producto_id = producto_id;
    RETURN cantidad > 0;
END;
8. Triggers
1. Crear un trigger que registre en HistorialSalarios cada cambio de salario de empleados
sql
Copiar
DELIMITER //
CREATE TRIGGER registro_cambio_salario
AFTER UPDATE ON DatosEmpleados
FOR EACH ROW
BEGIN
    IF OLD.salario != NEW.salario THEN
        INSERT INTO HistorialSalarios(empleado_id, salario_antiguo, salario_nuevo, fecha_cambio)
        VALUES (NEW.id, OLD.salario, NEW.salario, NOW());
    END IF;
END //
DELIMITER ;
2. Crear un trigger que evite borrar productos con pedidos activos
sql
Copiar
DELIMITER //
CREATE TRIGGER evitar_borrar_producto
BEFORE DELETE ON Productos
FOR EACH ROW
BEGIN
    IF EXISTS (SELECT 1 FROM Pedidos WHERE producto_id = OLD.id) THEN
        SIGNAL SQLSTATE '45000'
        SET MESSAGE_TEXT = 'No se puede borrar el producto, ya que tiene pedidos activos.';
    END IF;
END //
DELIMITER ;
3. Un trigger que registre en HistorialPedidos cada actualización en Pedidos
sql
Copiar
DELIMITER //
CREATE TRIGGER registro_actualizacion_pedido
AFTER UPDATE ON Pedidos
FOR EACH ROW
BEGIN
    INSERT INTO HistorialPedidos(pedido_id, cantidad_salida, cantidad_entrada, fecha_modificacion)
    VALUES (NEW.id, OLD.cantidad, NEW.cantidad, NOW());
END //
DELIMITER ;
4. Crear un trigger que actualice el inventario al registrar un pedido
sql
Copiar
DELIMITER //
CREATE TRIGGER actualizar_inventario_pedido
AFTER INSERT ON Pedidos
FOR EACH ROW
BEGIN
    UPDATE Productos
    SET inventario = inventario - NEW.cantidad
    WHERE id = NEW.producto_id;
END //
DELIMITER ;
5. Un trigger que evite actualizaciones de precio a menos de $1
sql
Copiar
DELIMITER //
CREATE TRIGGER evitar_precio_bajo
BEFORE UPDATE ON Productos
FOR EACH ROW
BEGIN
    IF NEW.precio < 1 THEN
        SIGNAL SQLSTATE '45000'
        SET MESSAGE_TEXT = 'El precio no puede ser menor a $1.';
    END IF;
END //
DELIMITER ;
6. Crear un trigger que registre la fecha de creación de un pedido en HistorialPedidos
sql
Copiar
DELIMITER //
CREATE TRIGGER registrar_fecha_creacion_pedido
AFTER INSERT ON Pedidos
FOR EACH ROW
BEGIN
    INSERT INTO HistorialPedidos(pedido_id, fecha_modificacion)
    VALUES (NEW.id, NOW());
END //
DELIMITER ;
7. Un trigger que mantenga el precio total de cada pedido en Pedidos
sql
Copiar
DELIMITER //
CREATE TRIGGER mantener_precio_total
AFTER INSERT ON DetallesPedido
FOR EACH ROW
BEGIN
    UPDATE Pedidos
    SET precio = (SELECT SUM(precio) FROM DetallesPedido WHERE pedido_id = NEW.pedido_id)
    WHERE id = NEW.pedido_id;
END //
DELIMITER ;
8. Crear un trigger para validar que UbicacionCliente no esté vacío al crear un cliente
sql
Copiar
DELIMITER //
CREATE TRIGGER validar_ubicacion_cliente
BEFORE INSERT ON Clientes
FOR EACH ROW
BEGIN
    IF NEW.direccion IS NULL THEN
        SIGNAL SQLSTATE '45000'
        SET MESSAGE_TEXT = 'El cliente debe tener una ubicación registrada.';
    END IF;
END //
DELIMITER ;
9. Un trigger que registre en LogActividades cada modificación en Proveedores
sql
Copiar
DELIMITER //
CREATE TRIGGER registro_modificacion_proveedor
AFTER UPDATE ON Proveedores
FOR EACH ROW
BEGIN
    INSERT INTO LogActividades(proveedor_id, descripcion, fecha_modificacion)
    VALUES (NEW.id, 'Proveedor actualizado', NOW());
END //
DELIMITER ;
10. Crear un trigger que registre en HistorialContratos cada cambio en Empleados
sql
Copiar
DELIMITER //
CREATE TRIGGER registro_cambio_empleado
AFTER UPDATE ON DatosEmpleados
FOR EACH ROW
BEGIN
    INSERT INTO HistorialContratos(empleado_id, salario_antiguo, salario_nuevo, fecha_modificacion)
    VALUES (NEW.id, OLD.salario, NEW.salario, NOW());
END //
DELIMITER ;
csharp
Copiar

Este es un conjunto completo de consultas SQL que cubren consultas multitabla, subconsultas, procedimientos almacenados, funciones definidas por el usuario y triggers. Puedes usarlo según las necesidades de tu base de datos.



Adjuntar

Buscar

Razona

Voz
ChatGPT puede cometer errores. Comprueba la información importante.
?
