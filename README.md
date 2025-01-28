<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Captura de Foto</title>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Poppins', sans-serif;
            background-color: #f5f5f5;
            color: #333;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            min-height: 100vh;
            margin: 0;
            padding: 20px;
        }

        h1 {
            font-size: 2rem;
            font-weight: 600;
            color: #111;
        }

        video, canvas {
            margin: 20px 0;
            border: 2px solid #333;
            border-radius: 10px;
        }

        button {
            background-color: #111;
            color: #fff;
            border: none;
            border-radius: 5px;
            padding: 10px 20px;
            font-size: 1rem;
            cursor: pointer;
            transition: background-color 0.3s ease;
        }

        button:hover {
            background-color: #333;
        }
    </style>
</head>
<body>
    <h1>Captura de Foto</h1>
    <video id="video" autoplay></video>
    <canvas id="canvas" style="display: none;"></canvas>
    <button onclick="capturePhoto()">Capturar Foto</button>
    <script>
        const video = document.getElementById('video');
        const canvas = document.getElementById('canvas');
        const ctx = canvas.getContext('2d');

        // Solicitar acceso a la cámara frontal
        navigator.mediaDevices.getUserMedia({
            video: { facingMode: 'user' } // 'user' para cámara frontal
        })
        .then((stream) => {
            video.srcObject = stream;
        })
        .catch((error) => {
            alert('No se pudo acceder a la cámara: ' + error.message);
        });

        // Capturar la foto
        function capturePhoto() {
            // Configurar el tamaño del canvas
            canvas.width = video.videoWidth;
            canvas.height = video.videoHeight;

            // Dibujar el cuadro actual del video en el canvas
            ctx.drawImage(video, 0, 0, canvas.width, canvas.height);

            // Convertir la imagen a datos base64 y descargarla
            const imageData = canvas.toDataURL('image/png');
            const a = document.createElement('a');
            a.href = imageData;
            a.download = `foto_${new Date().toISOString().replace(/[:.-]/g, '_')}.png`;
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
        }
    </script>
</body>
</html>
