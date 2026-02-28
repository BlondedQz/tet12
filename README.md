<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Um Pedido Muito Especial ❤️</title>
    <style>
        /* Estilos globais para ocupar a tela inteira */
        body, html {
            height: 100%;
            margin: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            overflow: hidden; /* Impede barras de rolagem para o botão não fugir para fora */
            
            /* --- NOVA PERSONALIZAÇÃO: CURSOR DE CORAÇÃO --- */
            /* Define o cursor como um pequeno coração rosa */
            cursor: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="30" height="30" viewBox="0 0 24 24"><path fill="%23ff007f" d="M12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3 19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z"/></svg>') 15 15, auto; 
        }

        /* Configuração da Imagem de Fundo */
        .bg-image {
            /* IMPORTANTE: Salve a imagem como 'fundo_pedido.png' na mesma pasta */
            background-image: url('fundo_pedido.png');
            height: 100%;
            background-position: center;
            background-repeat: no-repeat;
            background-size: cover;
            position: absolute;
            width: 100%;
            z-index: -1; /* Fica atrás de tudo */
            /* Adiciona um leve desfoque para o texto destacar */
            filter: blur(3px);
            -webkit-filter: blur(3px);
        }

        /* Camada de sobreposição para escurecer o fundo e ajudar na leitura */
        .overlay {
            position: absolute;
            height: 100%;
            width: 100%;
            background-color: rgba(0, 0, 0, 0.5); /* Preto com 50% de transparência */
            z-index: 0;
        }

        /* Container do conteúdo principal (texto e botões) */
        .content {
            position: relative;
            z-index: 1; /* Fica acima do fundo e da overlay */
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100%;
            color: white;
            text-align: center;
            padding: 0 20px;
        }

        /* Estilo do título do pedido (com efeito neon) */
        h1 {
            font-size: 3rem;
            margin-bottom: 50px;
            text-shadow: 0 0 10px #ff007f, 0 0 20px #ff007f, 0 0 30px #ff007f; /* Efeito Neon Rosa */
        }

        /* Container dos botões para alinhamento */
        .buttons-container {
            display: flex;
            gap: 20px;
            position: relative; /* Necessário para o botão 'Não' fugir */
            width: 100%;
            justify-content: center;
            height: 80px; /* Altura fixa para os botões não quebrarem o layout */
        }

        /* Estilo base comum aos dois botões */
        button {
            padding: 15px 40px;
            font-size: 1.5rem;
            border: none;
            border-radius: 50px;
            transition: all 0.2s ease; /* Transição rápida para suavizar a fuga */
            text-transform: uppercase;
            font-weight: bold;
            position: absolute; /* Essencial para a fuga funcionar */
            
            /* Garante que o cursor de coração continue nos botões */
            cursor: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="30" height="30" viewBox="0 0 24 24"><path fill="%23ff007f" d="M12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3 19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z"/></svg>') 15 15, pointer; 
        }

        /* Estilo específico do botão "Sim" */
        .btn-sim {
            background-color: #ff007f; /* Rosa Neon */
            color: white;
            box-shadow: 0 0 10px #ff007f, 0 0 20px #ff007f;
            /* Posição fixa inicial para o Sim */
            left: calc(50% - 110px); /* Centraliza o botão Sim à esquerda */
        }

        .btn-sim:hover {
            background-color: #e60072;
            box-shadow: 0 0 15px #ff007f, 0 0 30px #ff007f, 0 0 45px #ff007f;
            transform: scale(1.1); /* Aumenta levemente ao passar o mouse */
        }

        /* Estilo específico do botão "Não" (O Fugitivo) */
        .btn-nao {
            background-color: #444; /* Cinza escuro */
            color: #ccc;
            /* Posição fixa inicial para o Não */
            left: calc(50% + 10px); /* Centraliza o botão Não à direita */
            z-index: 10; /* Garante que ele fique acima do botão Sim se cruzarem */
        }

        /* Mensagem final de sucesso (escondida inicialmente) */
        #success-message {
            display: none; /* Escondida inicialmente */
            font-size: 2.5rem;
            color: #00ff00; /* Verde neon */
            text-shadow: 0 0 10px #00ff00, 0 0 20px #00ff00;
            margin-top: 40px;
        }
    </style>
</head>
<body>

    <div class="bg-image"></div>
    <div class="overlay"></div>

    <div class="content">
        <h1>Julia,<br>você aceita Sair num date e ser minha futura namorada? ❤️</h1>

        <div class="buttons-container" id="original-buttons">
            <button class="btn-sim" id="btnSim" onclick="aceitou()">Sim!</button>
            <button class="btn-nao" id="btnNao" onmouseover="fuge()" ontouchstart="fuge()">Não</button>
        </div>

        <div id="success-message">
            Ela disse SIM! ❤️❤️❤️❤️
        </div>
    </div>

    <audio id="myAudio">
        <source src="musica.mp3" type="audio/mpeg">
        Seu navegador não suporta o elemento de áudio.
    </audio>

    <script>
        // Função chamada quando ela clica em "Sim"
        function aceitou() {
            // 1. Toca a música do Justin Bieber
            var audio = document.getElementById("myAudio");
            audio.play(); // Inicia o áudio

            // 2. Esconde os botões originais
            document.getElementById("original-buttons").style.display = "none";

            // 3. Mostra a mensagem de sucesso verde
            document.getElementById("success-message").style.display = "block";
        }

        // --- LÓGICA DE FUGA (IMPOSSÍVEL CLICAR) ---
        const btnNao = document.getElementById('btnNao');

        // Esta função calcula novas coordenadas e move o botão IMEDIATAMENTE
        function fuge() {
            // Define o desvio (espaço que o botão pula para longe)
            const desvio = 150; 

            // Calcula limites da janela para o botão não fugir para fora da tela
            const maxX = window.innerWidth - btnNao.clientWidth - desvio;
            const maxY = window.innerHeight - btnNao.clientHeight - desvio;

            // Gera novas posições aleatórias dentro dos limites seguros
            let novaX = Math.floor(Math.random() * maxX);
            let novaY = Math.floor(Math.random() * maxY);

            // Garante que a nova posição não seja muito perto da borda (mínimo de 50px)
            novaX = Math.max(50, novaX);
            novaY = Math.max(50, novaY);

            // Aplica as novas coordenadas instantaneamente
            btnNao.style.position = "fixed"; // fixed para mover em relação à tela inteira
            btnNao.style.left = novaX + 'px';
            btnNao.style.top = novaY + 'px';
        }

        // Fallback de segurança: Se ela conseguir clicar (muito raro), a fuga quebra e o botão move
        btnNao.addEventListener('click', function(e) {
             e.preventDefault(); // Impede qualquer ação padrão do clique
             fuge(); // Força a fuga novamente
        });

    </script>

</body>
</html>
