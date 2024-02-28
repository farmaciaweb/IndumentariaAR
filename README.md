<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Registro de Productos</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: #f4f4f4;
            margin: 0;
            padding: 20px;
            text-align: center;
        }

        #productos {
            background-color: #fff;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            padding: 20px;
            margin-top: 20px;
        }

        form {
            max-width: 400px;
            margin: 20px auto;
            background-color: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }

        label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
        }

        input {
            width: 100%;
            padding: 8px;
            margin-bottom: 16px;
            box-sizing: border-box;
            border: 1px solid #ccc;
            border-radius: 4px;
        }

        button {
            background-color: #4caf50;
            color: #fff;
            padding: 10px 15px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }

        button:hover {
            background-color: #45a049;
        }

        ul {
            list-style-type: none;
            padding: 0;
        }

        li {
            margin-bottom: 10px;
            font-size: 16px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        a {
            color: #3498db;
            text-decoration: none;
            font-weight: bold;
        }

        a:hover {
            text-decoration: underline;
        }

        .eliminar {
            background-color: #e74c3c;
            color: #fff;
            padding: 5px 10px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <img src="INICIO.jpg" alt="Logo" style="max-width: 100%; height: auto;">
    <h2>Registro de Productos</h2>

    <form id="formularioProductos">
        <label for="nombreProducto">Nombre del Producto:</label>
        <input type="text" id="nombreProducto" required>
        <br>
        <label for="precioProducto">Precio del Producto:</label>
        <input type="number" id="precioProducto" required>

        <button type="button" onclick="cargarProducto()">Cargar Producto</button>
    </form>

    <div id="productos">
        <h3>Productos Cargados</h3>
        <ul id="listaProductos"></ul>
    </div>

    <p>¡Síguenos en <a href="https://www.instagram.com/indumentaria_ar/" target="_blank">Instagram</a> para más novedades!</p>

    <script>
        // Cargar productos almacenados en localStorage al cargar la página
        window.onload = function() {
            cargarProductosAlmacenados();
        };

        function cargarProductosAlmacenados() {
            var productos = JSON.parse(localStorage.getItem('productos')) || [];
            var listaProductos = document.getElementById("listaProductos");

            // Limpiar la lista antes de agregar los productos almacenados
            listaProductos.innerHTML = "";

            productos.forEach(function(producto) {
                var listItem = document.createElement("li");
                listItem.innerHTML = "<strong>" + producto.nombre + "</strong> - Precio: $" + producto.precio +
                                     "<button class='eliminar' onclick='eliminarProducto(\"" + producto.nombre + "\")'>Eliminar</button>";
                listaProductos.appendChild(listItem);
            });
        }

        function cargarProducto() {
            var nombreProducto = document.getElementById("nombreProducto").value;
            var precioProducto = document.getElementById("precioProducto").value;

            if (nombreProducto === "" || precioProducto === "") {
                alert("Por favor, completa todos los campos.");
                return;
            }

            // Crear un objeto con el nombre y precio del producto
            var nuevoProducto = {
                nombre: nombreProducto,
                precio: precioProducto
            };

            // Obtener productos almacenados en localStorage
            var productos = JSON.parse(localStorage.getItem('productos')) || [];

            // Agregar el nuevo producto al array de productos
            productos.push(nuevoProducto);

            // Guardar el array actualizado en localStorage
            localStorage.setItem('productos', JSON.stringify(productos));

            // Actualizar la lista de productos en la página
            cargarProductosAlmacenados();

            // Limpiar los campos del formulario después de cargar el producto
            document.getElementById("nombreProducto").value = "";
            document.getElementById("precioProducto").value = "";
        }

        function eliminarProducto(nombreProducto) {
            // Obtener productos almacenados en localStorage
            var productos = JSON.parse(localStorage.getItem('productos')) || [];

            // Filtrar el producto a eliminar por nombre
            productos = productos.filter(function(producto) {
                return producto.nombre !== nombreProducto;
            });

            // Guardar el array actualizado en localStorage
            localStorage.setItem('productos', JSON.stringify(productos));

            // Actualizar la lista de productos en la página
            cargarProductosAlmacenados();
        }
    </script>
</body>
</html>
