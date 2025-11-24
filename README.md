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
