document.addEventListener('DOMContentLoaded', function () {
    const formulario = document.getElementById('formulario');
    const tbodyInventario = document.querySelector('#inventario-tabla tbody');

    const producto = [
        { id: 1, nombre: "Laptop Dell XPS 15", marca: "Dell", stock: 5, precio: 1500 },
        { id: 2, nombre: "Smartphone iPhone 14", marca: "Apple", stock: 8, precio: 1200 },
        { id: 3, nombre: "Monitor UltraSharp 27\"", marca: "Dell", stock: 3, precio: 350 },
        { id: 4, nombre: "Teclado mecánico K95", marca: "Corsair", stock: 10, precio: 180 },
        { id: 5, nombre: "Auriculares WH-1000XM4", marca: "Sony", stock: 6, precio: 300 },
        { id: 6, nombre: "Tablet Galaxy Tab S8", marca: "Samsung", stock: 4, precio: 800 },
        { id: 7, nombre: "Cámara Mirrorless Alpha 7 IV", marca: "Sony", stock: 2, precio: 2500 },
        { id: 8, nombre: "Router WiFi 6 AX6000", marca: "TP-Link", stock: 7, precio: 220 },
        { id: 9, nombre: "Disco SSD NVMe 1TB", marca: "Samsung", stock: 15, precio: 130 },
        { id: 10, nombre: "Mouse inalámbrico MX Master 3", marca: "Logitech", stock: 9, precio: 100 },
        { id: 11, nombre: "Auriculares Gaming Kraken X", marca: "Razer", stock: 12, precio: 60 },
        { id: 12, nombre: "Smartwatch Galaxy Watch 5", marca: "Samsung", stock: 5, precio: 250 },
        { id: 13, nombre: "Impresora láser HP LaserJet Pro", marca: "HP", stock: 3, precio: 400 },
        { id: 14, nombre: "Altavoces Bluetooth Soundcore", marca: "Anker", stock: 6, precio: 90 },
        { id: 15, nombre: "Microprocesador Ryzen 9 7900X", marca: "AMD", stock: 4, precio: 500 },
        { id: 16, nombre: "Tarjeta gráfica RTX 4070 Ti", marca: "NVIDIA", stock: 2, precio: 900 },
        { id: 17, nombre: "Smart TV OLED 55\"", marca: "LG", stock: 3, precio: 1800 },
        { id: 18, nombre: "Consola PlayStation 5", marca: "Sony", stock: 5, precio: 550 },
        { id: 19, nombre: "Consola Xbox Series X", marca: "Microsoft", stock: 4, precio: 500 },
        { id: 20, nombre: "Router Mesh Deco X60", marca: "TP-Link", stock: 8, precio: 300 },
        { id: 21, nombre: "Cámara de seguridad Arlo Pro 4", marca: "Arlo", stock: 5, precio: 350 },
        { id: 22, nombre: "Disco duro externo 5TB", marca: "Western Digital", stock: 6, precio: 180 },
        { id: 23, nombre: "Lámpara LED inteligente Philips Hue", marca: "Philips", stock: 7, precio: 75 },
        { id: 24, nombre: "Estación de carga USB-C 100W", marca: "Anker", stock: 10, precio: 120 }
    ];

    function AgregarProducto(producto) {
            const fila = document.createElement('tr');

            const celdaId = document.createElement('td');
            celdaId.textContent = producto.id;

            const celdaNombre = document.createElement('td');
            celdaNombre.textContent = producto.nombre;

            const celdaMarca = document.createElement('td');
            celdaMarca.textContent = producto.marca;

            const celdaStock = document.createElement('td');
            celdaStock.textContent = producto.stock;

            const celdaPrecio = document.createElement('td');
            celdaPrecio.textContent = `$${producto.precio}`;

            const celdaAcciones = document.createElement('td');
            celdaAcciones.innerHTML = `
                <button type="button" class="btn btn-warning text-white" data-toggle="modal" data-target="#staticBackdrop">
                    <i class="fa-solid fa-pen-to-square"></i>
                </button>
                <button class="btn btn-danger">
                    <i class="fa-solid fa-trash"></i>
                </button>`;

            fila.append(celdaId, celdaNombre, celdaMarca, celdaStock, celdaPrecio, celdaAcciones);
            tbodyInventario.append(fila);
    };
    
    producto.forEach(AgregarProducto);

    formulario.addEventListener('submit', function (event) {
        event.preventDefault();

        const inputNombre = document.getElementById('nombre');
        const inputMarca = document.getElementById('marca');
        const inputCantidad = document.getElementById('cantidad');
        const inputPrecio = document.getElementById('precio');

        const nombre = inputNombre.value.trim();
        const marca = inputMarca.value.trim();
        const cantidad = parseInt(inputCantidad.value);
        const precio = parseFloat(inputPrecio.value);

        let esValido = true;

        // Validaciones
        if (nombre.length < 3 || nombre.length > 20) {
            alert('El nombre debe tener entre 3 y 20 caracteres.');
            inputNombre.classList.add('is-invalid');
            esValido = false;
        }
        if (marca.length < 3 || marca.length > 20) {
            alert('La marca debe tener entre 3 y 20 caracteres.');
            inputMarca.classList.add('is-invalid');
            esValido = false;
        }
        if (isNaN(cantidad) || cantidad < 0) {
            alert('La cantidad debe ser un número positivo.');
            inputCantidad.classList.add('is-invalid');
            esValido = false;
        }
        if (isNaN(precio) || precio < 0) {
            alert('El precio debe ser un número positivo.');
            inputPrecio.classList.add('is-invalid');
            esValido = false;
        }

        if (!esValido) return;

        // Crear producto nuevo
        const nuevoProducto = {
            id: Math.max(...producto.map(s => s.id)) + 1,
            nombre,
            marca,
            stock: cantidad,
            precio
        };

        producto.push(nuevoProducto);
        AgregarProducto(nuevoProducto);
        formulario.reset();

        // Limpiar clases de validación
        [inputNombre, inputMarca, inputCantidad, inputPrecio].forEach(input => {
            input.classList.remove('is-invalid');
        });
    });
});
