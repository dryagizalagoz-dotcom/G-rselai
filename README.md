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
