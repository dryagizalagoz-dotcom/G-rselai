# G-rselai
A ai use open ai to make photos
<!DOCTYPE html>
<html lang="tr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>GörselYZ</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <div class="container">
    <h1>GörselYZ</h1>
    <textarea id="prompt" placeholder="Buraya promptunu yaz..."></textarea>
    <button id="generateBtn">Görseli Üret</button>
    <div id="progressBarContainer">
      <div id="progressBar"></div>
    </div>
    <div id="result"></div>
    <h3>Örnek Görseller</h3>
    <div class="slider">
      <img src="https://picsum.photos/id/237/200/200" alt="">
      <img src="https://picsum.photos/id/238/200/200" alt="">
      <img src="https://picsum.photos/id/239/200/200" alt="">
    </div>
  </div>
  <script src="script.js"></script>
</body>
</html>
body {
  font-family: Arial, sans-serif;
  background: #f4f4f4;
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  margin: 0;
}

.container {
  background: #fff;
  padding: 20px;
  border-radius: 12px;
  width: 90%;
  max-width: 500px;
  text-align: center;
  box-shadow: 0 4px 10px rgba(0,0,0,0.1);
}

textarea {
  width: 100%;
  height: 100px;
  border-radius: 8px;
  padding: 10px;
  border: 1px solid #ccc;
  resize: none;
  font-size: 16px;
  margin-bottom: 10px;
}

button {
  padding: 10px 20px;
  font-size: 16px;
  border: none;
  border-radius: 8px;
  background-color: #4caf50;
  color: white;
  cursor: pointer;
  margin-bottom: 10px;
}

button:hover {
  background-color: #45a049;
}

#progressBarContainer {
  width: 100%;
  height: 10px;
  background-color: #ddd;
  border-radius: 5px;
  overflow: hidden;
  margin: 10px 0;
  display: none;
}

#progressBar {
  height: 100%;
  width: 0%;
  background-color: #4caf50;
  transition: width 0.3s;
}

#result img {
  max-width: 100%;
  margin-top: 10px;
  border-radius: 8px;
}

.slider {
  display: flex;
  overflow-x: auto;
  gap: 10px;
  margin-top: 10px;
}

.slider img {
  border-radius: 8px;
  width: 100px;
  height: 100px;
  object-fit: cover;
  flex-shrink: 0;
  transition: transform 0.3s;
}

.slider img:hover {
  transform: scale(1.1);
}
const generateBtn = document.getElementById("generateBtn");
const promptInput = document.getElementById("prompt");
const resultDiv = document.getElementById("result");
const progressBarContainer = document.getElementById("progressBarContainer");
const progressBar = document.getElementById("progressBar");

let userQuota = 3; // Her kullanıcı için 3 görsel hakkı

generateBtn.addEventListener("click", async () => {
  const prompt = promptInput.value.trim();
  if (!prompt) {
    alert("Lütfen bir prompt yaz!");
    return;
  }
  if (userQuota <= 0) {
    alert("Üzgünüz, günlük görsel hakkınızı kullandınız!");
    return;
  }

  // Loading bar göster
  progressBarContainer.style.display = "block";
  progressBar.style.width = "0%";

  // Simülasyon: loading bar 3 saniye
  let width = 0;
  const interval = setInterval(() => {
    width += 5;
    progressBar.style.width = width + "%";
    if (width >= 100) clearInterval(interval);
  }, 150);

  try {
    const res = await fetch("/api/generate", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify({ prompt }),
    });

    const data = await res.json();
    const img = document.createElement("img");
    img.src = data.image;
    resultDiv.innerHTML = "";
    resultDiv.appendChild(img);

    userQuota--;
  } catch (err) {
    alert("Bir hata oluştu, tekrar deneyin!");
    console.error(err);
  } finally {
    progressBarContainer.style.display = "none";
    progressBar.style.width = "0%";
  }
});
import OpenAI from "openai";

const openai = new OpenAI({
  apiKey: process.env.OPENAI_API_KEY // Vercel’de Environment Variable olarak ekle
});

export default async function handler(req, res) {
  if (req.method !== "POST") {
    return res.status(405).json({ error: "Sadece POST desteklenir" });
  }

  const { prompt } = req.body;

  if (!prompt) {
    return res.status(400).json({ error: "Prompt boş olamaz" });
  }

  try {
    const response = await openai.images.generate({
      model: "gpt-image-1",
      prompt: prompt,
      size: "512x512"
    });

    const image_url = response.data[0].url;
    res.status(200).json({ image: image_url });
  } catch (error) {
    console.error(error);
    res.status(500).json({ error: "Görsel üretilemedi" });
  }
}0
