<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <title>Rastreador p5.js</title>
  <script src="https://cdn.jsdelivr.net/npm/@fingerprintjs/fingerprintjs@3/dist/fp.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/p5@1.6.0/lib/p5.min.js"></script>
</head>
<body>
<script>
  let visitorId = '';
  let userIP = '';

  function setup() {
    createCanvas(400, 200);
    background(220);
    textAlign(CENTER, CENTER);
    textSize(16);

    FingerprintJS.load().then(fp => {
      fp.get().then(result => {
        visitorId = result.visitorId;
        console.log('Fingerprint:', visitorId);
        sendData();
      });
    });

    fetch('https://api.ipify.org?format=json')
      .then(response => response.json())
      .then(data => {
        userIP = data.ip;
        console.log('IP:', userIP);
        sendData();
      });
  }

  function draw() {
    background(220);
    text('Fingerprint:\n' + visitorId, width / 2, height / 3);
    text('IP:\n' + userIP, width / 2, height / 2);
  }

  // Função para enviar dados a um servidor (exemplo)
  function sendData() {
    if (visitorId && userIP) {
      // Aqui você enviaria para seu servidor via fetch POST
      console.log('Enviando dados:', visitorId, userIP);
      // Exemplo:
      // fetch('https://seuservidor.com/rastreador', {
      //   method: 'POST',
      //   headers: {'Content-Type': 'application/json'},
      //   body: JSON.stringify({visitorId, userIP, timestamp: Date.now()})
      // });
    }
  }
</script>
</body>
</html>
