# cicero-camera
<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Cicero Camera</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      background-color: #f4f4f9;
      padding: 20px;
    }
    h1 { color: #333; }
    #video {
      width: 100%;
      max-width: 500px;
      border: 3px solid #333;
      border-radius: 8px;
      background: #000;
    }
    button {
      padding: 10px 20px;
      font-size: 16px;
      margin-top: 15px;
      cursor: pointer;
      border: none;
      border-radius: 5px;
      background-color: #28a745;
      color: white;
    }
    button:hover { background-color: #218838; }
  </style>
</head>
<body>

  <h1>cicero-camera</h1>
  <video id="video" autoplay playsinline></video>
  <br>
  <button id="start-btn">Mở Camera</button>

  <script>
    const video = document.getElementById('video');
    const startBtn = document.getElementById('start-btn');

    startBtn.addEventListener('click', async () => {
      try {
        const stream = await navigator.mediaDevices.getUserMedia({ video: true, audio: false });
        video.srcObject = stream;
      } catch (err) {
        alert('Không thể truy cập camera: ' + err.message);
      }
    });
  </script>

</body>
</html>
