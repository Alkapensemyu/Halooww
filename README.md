<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>WOW Visual Effect</title>
  <link rel="stylesheet" href="style.css" />
</head>
<body>
  <div class="container">
    <h1 class="glitch" onclick="playSound()">WOW!</h1>
    <p>Gerakkan mouse dan klik untuk melihat efek!</p>
  </div>
  <canvas id="particles"></canvas>
  <audio id="clickSound" src="sound/click.mp3"></audio>
  <script src="script.js"></script>
</body>
</html>
