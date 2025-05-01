# T1-Dise-o
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Registro de Estudiantes</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 600px;
            margin: 0 auto;
            padding: 20px;
            background-color: #f5f5f5;
        }
        h1 {
            color: #2c3e50;
            text-align: center;
        }
        .form-container, .view-container {
            background-color: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
            margin-bottom: 20px;
        }
        label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
        }
        input[type="text"],
        input[type="date"],
        input[type="tel"] {
            width: 100%;
            padding: 8px;
            margin-bottom: 15px;
            border: 1px solid #ddd;
            border-radius: 4px;
            box-sizing: border-box;
        }
        button {
            background-color: #3498db;
            color: white;
            border: none;
            padding: 10px 15px;
            border-radius: 4px;
            cursor: pointer;
            font-size: 16px;
        }
        button:hover {
            background-color: #2980b9;
        }
        .data-display {
            margin-bottom: 15px;
            padding: 10px;
            background-color: #f9f9f9;
            border-left: 4px solid #3498db;
        }
        .hidden {
            display: none;
        }
        .countdown {
            text-align: center;
            font-size: 18px;
            color: #7f8c8d;
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <h1>Registrar los datos de un estudiante</h1>
    
    <div id="formContainer" class="form-container">
        <form id="studentForm">
            <label for="nombres">Nombres:</label>
            <input type="text" id="nombres" name="nombres" required>
            
            <label for="apellidos">Apellidos:</label>
            <input type="text" id="apellidos" name="apellidos" required>
            
            <label for="fechaNacimiento">Fecha de Nacimiento:</label>
            <input type="date" id="fechaNacimiento" name="fechaNacimiento" required>
            
            <label for="direccion">Dirección:</label>
            <input type="text" id="direccion" name="direccion" required>
            
            <label for="telefono">Teléfono:</label>
            <input type="tel" id="telefono" name="telefono" required>
            
            <button type="submit">Registrar Estudiante</button>
        </form>
    </div>
    
    <div id="viewContainer" class="view-container hidden">
        <h2>Datos del Estudiante Registrado</h2>
        <div class="data-display">
            <p><strong>Nombres:</strong> <span id="viewNombres"></span></p>
            <p><strong>Apellidos:</strong> <span id="viewApellidos"></span></p>
            <p><strong>Fecha de Nacimiento:</strong> <span id="viewFechaNacimiento"></span></p>
            <p><strong>Dirección:</strong> <span id="viewDireccion"></span></p>
            <p><strong>Teléfono:</strong> <span id="viewTelefono"></span></p>
        </div>
        <div class="countdown">
            Volviendo al formulario en <span id="countdown">7</span> segundos...
        </div>
    </div>

    <script>
        const studentForm = document.getElementById('studentForm');
        const formContainer = document.getElementById('formContainer');
        const viewContainer = document.getElementById('viewContainer');
        const countdownElement = document.getElementById('countdown');
        
        studentForm.addEventListener('submit', function(e) {
            e.preventDefault();
            
            // Obtener los valores del formulario
            const nombres = document.getElementById('nombres').value;
            const apellidos = document.getElementById('apellidos').value;
            const fechaNacimiento = document.getElementById('fechaNacimiento').value;
            const direccion = document.getElementById('direccion').value;
            const telefono = document.getElementById('telefono').value;
            
            // Mostrar los datos en la vista
            document.getElementById('viewNombres').textContent = nombres;
            document.getElementById('viewApellidos').textContent = apellidos;
            document.getElementById('viewFechaNacimiento').textContent = formatDate(fechaNacimiento);
            document.getElementById('viewDireccion').textContent = direccion;
            document.getElementById('viewTelefono').textContent = telefono;
            
            // Cambiar a la vista de visualización
            formContainer.classList.add('hidden');
            viewContainer.classList.remove('hidden');
            
            // Iniciar cuenta regresiva
            let seconds = 7;
            countdownElement.textContent = seconds;
            
            const countdownInterval = setInterval(() => {
                seconds--;
                countdownElement.textContent = seconds;
                
                if (seconds <= 0) {
                    clearInterval(countdownInterval);
                    resetForm();
                }
            }, 1000);
        });
        
        function formatDate(dateString) {
            if (!dateString) return '';
            const date = new Date(dateString);
            return date.toLocaleDateString('es-ES');
        }
        
        function resetForm() {
            // Limpiar el formulario
            studentForm.reset();
            
            // Volver a mostrar el formulario
            viewContainer.classList.add('hidden');
            formContainer.classList.remove('hidden');
        }
    </script>
</body>
</html>
