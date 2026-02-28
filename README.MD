<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Um Pedido Muito Especial ❤️</title>

  <style>
    /* ===== RESET E CONFIGURAÇÃO GLOBAL ===== */
    body, html {
      height: 100%;
      margin: 0;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      overflow: hidden;
      cursor: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="30" height="30" viewBox="0 0 24 24"><path fill="%23ff007f" d="M12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3 19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z"/></svg>') 15 15, auto;
    }

    /* ===== FUNDO ===== */
    .bg-image {
      background: url('fundo_pedido.png') center/cover no-repeat;
      position: absolute;
      width: 100%;
      height: 100%;
      z-index: -1;
      filter: blur(3px);
    }

    .overlay {
      position: absolute;
      width: 100%;
      height: 100%;
      background: rgba(0, 0, 0, 0.5);
      z-index: 0;
    }

    /* ===== CONTEÚDO ===== */
    .content {
      position: relative;
      z-index: 1;
      height: 100%;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      text-align: center;
      color: white;
      padding: 20px;
    }

    h1 {
      font-size: 3rem;
      margin-bottom: 50px;
      text-shadow: 0 0 10px #ff007f,
                   0 0 20px #ff007f,
                   0 0 30px #ff007f;
    }

    /* ===== BOTÕES ===== */
    .buttons-container {
      position: relative;
      width: 100%;
      height: 80px;
      display: flex;
      justify-content: center;
      gap: 20px;
    }

    button {
      position: absolute;
      padding: 15px 40px;
      font-size: 1.5rem;
      border: none;
      border-radius: 50px;
      font-weight: bold;
      text-transform: uppercase;
      transition: 0.2s ease;
      cursor: pointer;
    }

    .btn-sim {
      background: #ff007f;
      color: white;
      left: calc(50% - 110px);
      box-shadow: 0 0 10px #ff007f,
                  0 0 20px #ff007f;
    }

    .btn-sim:hover {
      transform: scale(1.1);
      box-shadow: 0 0 20px #ff007f,
                  0 0 40px #ff007f;
    }

    .btn-nao {
      background: #444;
      color: #ccc;
      left: calc(50% + 10px);
      z-index: 10;
    }

    /* ===== MENSAGEM FINAL ===== */
    #success-message {
      display: none;
      margin-top: 40px;
      font-size: 2.5rem;
      color: #00ff00;
      text-shadow: 0 0 10px #00ff00,
                   0 0 20px #00ff00;
    }
  </style>
</head>

<body>

  <div class="bg-image"></div>
  <div class="overlay"></div>

  <div class="content">
    <h1>
      Julia,<br>
      você aceita sair num date e ser minha futura namorada? ❤️
    </h1>

    <div class="buttons-container" id="buttons">
      <button class="btn-sim" onclick="aceitou()">Sim!</button>
      <button class="btn-nao" id="btnNao">Não</button>
    </div>

    <div id="success-message">
      Ela disse SIM! ❤️❤️❤️❤️
    </div>
  </div>

  <audio id="audio">
    <source src="musica.mp3" type="audio/mpeg">
  </audio>

  <script>
    const btnNao = document.getElementById('btnNao');

    function aceitou() {
      document.getElementById('audio').play();
      document.getElementById('buttons').style.display = "none";
      document.getElementById('success-message').style.display = "block";
    }

    function fugir() {
      const maxX = window.innerWidth - btnNao.clientWidth;
      const maxY = window.innerHeight - btnNao.clientHeight;

      const novaX = Math.random() * maxX;
      const novaY = Math.random() * maxY;

      btnNao.style.position = "fixed";
      btnNao.style.left = novaX + "px";
      btnNao.style.top = novaY + "px";
    }

    btnNao.addEventListener("mouseover", fugir);
    btnNao.addEventListener("touchstart", fugir);
    btnNao.addEventListener("click", e => {
      e.preventDefault();
      fugir();
    });
  </script>

</body>
</html>

