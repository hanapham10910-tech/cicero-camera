# cicero-camera
stream = null;
  }

  camera.srcObject = null;
  status.textContent = "Camera và micro chưa được bật";
  enable.disabled = false;
  stop.disabled = true;
};
</script>

</body>
</html>
<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Cicero Practice</title>

<style>
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: #f3f6fc;
  color: #172554;
}

header {
  background: #14264d;
  color: white;
  padding: 22px 20px;
}

header h1 {
  margin: 0;
  font-size: 26px;
}

header p {
  margin: 8px 0 0;
  color: #dbeafe;
}

main {
  max-width: 850px;
  margin: 35px auto;
  padding: 20px;
}

.intro {
  text-align: center;
  margin-bottom: 25px;
}

.intro h2 {
  font-size: 28px;
  margin-bottom: 10px;
}

.intro p {
  color: #64748b;
  line-height: 1.6;
}

.camera-box {
  background: #14264d;
  border-radius: 18px;
  padding: 12px;
  box-shadow: 0 8px 25px #14264d20;
}

video {
  width: 100%;
  aspect-ratio: 16 / 9;
  display: block;
  object-fit: cover;
  background: #0b1530;
  border-radius: 12px;
}

#status {
  text-align: center;
  color: #64748b;
  margin: 18px 0;
}

.buttons {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  gap: 12px;
}

button {
  border: none;
  border-radius: 10px;
  padding: 13px 20px;
  font-size: 15px;
  font-weight: bold;
  cursor: pointer;
}

#enable {
  background: #2563eb;
  color: white;
}

#stop {
  background: #e2e8f0;
  color: #1e293b;
}

button:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

footer {
  text-align: center;
  padding: 20px;
  color: #64748b;
  font-size: 13px;
}
</style>
</head>

<body>

<header>
  <h1>Cicero & Co.</h1>
  <p>Không gian luyện tập thuyết trình</p>
</header>

<main>
  <section class="intro">
    <h2>Luyện tập thuyết trình</h2>
    <p>
      Hãy chuẩn bị bài nói của bạn.
      Bật camera và micro để sẵn sàng luyện tập!
    </p>
  </section>

  <section class="camera-box">
    <video id="camera" autoplay muted playsinline></video>
  </section>

  <p id="status">Camera và micro chưa được bật</p>

  <div class="buttons">
    <button id="enable">Bật camera và micro</button>
    <button id="stop" disabled>Tắt camera và micro</button>
  </div>
</main>

<footer>
  CICERO & CO. — PRACTICE • SPEAK • IMPROVE
</footer>

<script>
let stream = null;

const camera = document.getElementById("camera");
const status = document.getElementById("status");
const enable = document.getElementById("enable");
const stop = document.getElementById("stop");

enable.onclick = async () => {
  try {
    stream = await navigator.mediaDevices.getUserMedia({
      video: true,
      audio: true
    });

    camera.srcObject = stream;
    status.textContent = "Camera và micro đang hoạt động";
    enable.disabled = true;
    stop.disabled = false;
  } catch (error) {
    status.textContent =
      "Không thể bật camera hoặc micro. Hãy kiểm tra quyền truy cập.";
  }
};

stop.onclick = () => {
  if (stream) {
    stream.getTracks().forEach(track => track.stop());
