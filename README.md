<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Obtener Ubicación</title>
    <script>
        function getLocation() {
            if (navigator.geolocation) {
                navigator.geolocation.getCurrentPosition(showPosition, showError);
            } else {
                alert("La geolocalización no es compatible con este navegador.");
            }
        }

        function showPosition(position) {
            const latitude = position.coords.latitude;
            const longitude = position.coords.longitude;
            const timestamp = new Date(position.timestamp);

            // Mostrar en pantalla
            document.getElementById("output").innerHTML = `
                <p><strong>Latitud:</strong> ${latitude}</p>
                <p><strong>Longitud:</strong> ${longitude}</p>
                <p><strong>Fecha y Hora:</strong> ${timestamp}</p>
            `;

            // Enviar datos a un servidor (opcional)
            // fetch('https://tu-servidor.com/api', {
            //     method: 'POST',
            //     body: JSON.stringify({ latitude, longitude, timestamp }),
            //     headers: { 'Content-Type': 'application/json' },
            // });
        }

        function showError(error) {
            switch (error.code) {
                case error.PERMISSION_DENIED:
                    alert("El usuario denegó la solicitud de geolocalización.");
                    break;
                case error.POSITION_UNAVAILABLE:
                    alert("La información de ubicación no está disponible.");
                    break;
                case error.TIMEOUT:
                    alert("La solicitud para obtener la ubicación ha expirado.");
                    break;
                case error.UNKNOWN_ERROR:
                    alert("Se produjo un error desconocido.");
                    break;
            }
        }
    </script>
</head>
<body>
    <h1>Obtener Ubicación Satelital</h1>
    <button onclick="getLocation()">Obtener Mi Ubicación</button>
    <div id="output" style="margin-top: 20px;"></div>
</body>
</html>

