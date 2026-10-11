# cicero-camera
<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Cicero - Luyện tập</title>

  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      padding: 20px;
    }

    video {
      width: 100%;
      max-width: 640px;
      background: #222;
      border-radius: 12px;
    }

    button {
      padding: 12px 18px;
      margin: 8px;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      font-size: 16px;
    }

    #start {
      background: #2563eb;
      color: white;
    }

    #stop {
      background: #ddd;
      color: #222;
    }
  </style>
</head>

<body>
  <h2>Cicero - Luyện tập thuyết trình</h2>

  <video id="camera" autoplay muted playsinline></video>

  <p id="status">Camera và micro chưa bật</p>

  <button id="start">Bật camera và micro</button>
  <button id="stop" disabled>Tắt camera và micro</button>

  <script>
    const camera = document.getElementById("camera");
    const status = document.getElementById("status");
    const start = document.getElementById("start");
    const stop = document.getElementById("stop");

    let stream = null;

    start.addEventListener("click", async () => {
      try {
        status.textContent = "Đang xin quyền camera và micro...";

        stream = await navigator.mediaDevices.getUserMedia({
          video: true,
          audio: true
        });

        camera.srcObject = stream;
        await camera.play();

        status.textContent = "Camera và micro đã được bật!";
        start.disabled = true;
        stop.disabled = false;

      } catch (error) {
        status.textContent =
          "Không bật được camera hoặc micro: " + error.name;

        console.error(error);
      }
    });

    stop.addEventListener("click", () => {
      if (stream) {
        stream.getTracks().forEach(track => track.stop());
        stream = null;
      }

      camera.srcObject = null;
      status.textContent = "Camera và micro chưa bật";
      start.disabled = false;
      stop.disabled = true;
    });
  </script>
</body>
</html>
