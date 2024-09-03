<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dosificación de Medicamentos</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            color: #333;
            padding: 20px;
        }
        .container {
            max-width: 800px;
            margin: 0 auto;
            background-color: #fff;
            padding: 20px;
            border-radius: 5px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        h1 {
            color: #5a8f5e;
        }
        label {
            font-weight: bold;
        }
        input[type="text"] {
            width: 100%;
            padding: 10px;
            margin: 10px 0;
            border: 1px solid #ccc;
            border-radius: 4px;
        }
        input[type="submit"] {
            background-color: #5a8f5e;
            color: white;
            padding: 10px 15px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }
        input[type="submit"]:hover {
            background-color: #4e7f51;
        }
        .result {
            margin-top: 20px;
            padding: 10px;
            background-color: #e7f9e7;
            border-left: 5px solid #5a8f5e;
        }
        .section {
            margin-top: 10px;
            margin-bottom: 10px;
        }
        .section strong {
            display: block;
            margin-bottom: 5px;
            color: #5a8f5e;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Dosificación de Medicamentos</h1>
        <form method="post">
            <label for="medicamento">Nombre del Medicamento:</label>
            <input type="text" id="medicamento" name="medicamento" required>
            <input type="submit" value="Consultar">
        </form>

        <?php
        if ($_SERVER["REQUEST_METHOD"] == "POST") {
            $medicamento = strtolower(trim($_POST["medicamento"]));

            // Datos de conexión a la base de datos
            $servername = "nombre_del_servidor.mysql.database.azure.com";
            $username = "tu_usuario";
            $password = "tu_contraseña";
            $dbname = "nombre_de_tu_base_de_datos";

            // Crear la conexión
            $conn = new mysqli($servername, $username, $password, $dbname);

            // Verificar la conexión
            if ($conn->connect_error) {
                die("Conexión fallida: " . $conn->connect_error);
            }

            // Consultar la información completa del medicamento
            $sql = "SELECT dosis, modo_administracion, contraindicaciones, interacciones, efectos_secundarios, precauciones, monitoreo, sobredosis, almacenamiento FROM medicamentos WHERE LOWER(nombre) = ?";
            $stmt = $conn->prepare($sql);
            $stmt->bind_param("s", $medicamento);
            $stmt->execute();
            $stmt->bind_result($dosis, $modo_administracion, $contraindicaciones, $interacciones, $efectos_secundarios, $precauciones, $monitoreo, $sobredosis, $almacenamiento);

            if ($stmt->fetch()) {
                echo "<div class='result'>
                    <div class='section'><strong>Dosis:</strong> $dosis</div>
                    <div class='section'><strong>Modo de administración:</strong> $modo_administracion</div>
                    <div class='section'><strong>Contraindicaciones:</strong> $contraindicaciones</div>
                    <div class='section'><strong>Interacciones:</strong> $interacciones</div>
                    <div class='section'><strong>Efectos secundarios:</strong> $efectos_secundarios</div>
                    <div class='section'><strong>Precauciones:</strong> $precauciones</div>
                    <div class='section'><strong>Monitoreo:</strong> $monitoreo</div>
                    <div class='section'><strong>Sobredosis:</strong> $sobredosis</div>
                    <div class='section'><strong>Almacenamiento:</strong> $almacenamiento</div>
                </div>";
            } else {
                echo "<div class='result'>Lo siento, no tenemos información sobre el medicamento <strong>" . ucfirst($medicamento) . "</strong>.</div>";
            }

            // Cerrar la conexión
            $stmt->close();
            $conn->close();
        }
        ?>
    </div>
</body>
</html>
