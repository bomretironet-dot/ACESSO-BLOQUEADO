<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Serviço Bloqueado - Ravinet</title>
  <style>
    body {
      margin: 0;
      font-family: 'Segoe UI', sans-serif;
      background: linear-gradient(to right, #0d1b2a, #1b263b);
      color: #1a1a1a;
    }
    /* Removido o estilo original do #hora-data do body */
    
    .container {
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 90vh;
    }
    .card {
      background-color: #ffb347;
      padding: 30px;
      border-radius: 12px;
      box-shadow: 0 12px 30px rgba(0, 0, 0, 0.3);
      text-align: center;
      max-width: 600px;
      width: 100%;
    }
    #hora-data {
      color: white;
      font-weight: bold;
      margin-bottom: 15px;
      font-size: 16px;
    }
    .titulo {
      font-size: 60px;
      color: #2ecc71;
      font-weight: 900;
      text-decoration: underline;
    }
    .mensagem {
      font-size: 18px;
      line-height: 1.6;
      margin: 18px 0;
    }
    .destaque {
      color: #b00000;
      font-weight: bold;
    }
    .btn {
      display: inline-block;
      margin: 10px;
      padding: 12px 20px;
      font-size: 16px;
      background-color: #1a1a1a;
      color: #ffffff;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      text-decoration: none;
    }
    .jogo-container {
      display: none;
      margin-top: 20px;
    }
    #gameArea {
      position: relative;
      width: 300px;
      height: 400px;
      margin: 0 auto;
      background-color: #fff;
      border: 2px solid #333;
      overflow: hidden;
      border-radius: 10px;
    }
    .balao {
      position: absolute;
      width: 40px;
      height: 60px;
      background-color: red;
      border-radius: 50% 50% 50% 50%;
      cursor: pointer;
      box-shadow: inset -2px -4px 0 rgba(0,0,0,0.2);
    }
    #score {
      font-size: 18px;
      margin-top: 10px;
    }
  </style>
</head>
<body>

  <div class="container">
    <div class="card">
      <div id="hora-data">Carregando data e hora...</div>

      <div class="titulo">Ravinet</div>
      <h1 style="font-size: 28px; color: #b00000;">Serviço Bloqueado por Falta de Pagamento</h1>
      <p class="mensagem">Olá, identificamos que sua mensalidade da <strong>Ravinet</strong> está em atraso há algum tempo.</p>
      <p class="mensagem">Por isso, seu serviço de internet foi <strong>bloqueado</strong> até que o pagamento seja regularizado.</p>
      <p class="mensagem destaque">Para restabelecer sua conexão, por favor, entre em contato com nosso atendimento e realize o pagamento pendente.</p>
      
      <a class="btn" id="zap" target="_blank">Falar com Suporte (WhatsApp)</a>
      <button class="btn" id="jogarBtn">Jogar enquanto espero</button>

      <div class="jogo-container" id="jogo">
        <div id="gameArea"></div>
        <div id="score">Pontuação: 0</div>
      </div>

      <div style="margin-top: 30px; font-size: 14px; color: #2e2e2e;">
        Agradecemos a compreensão.<br />© 2025 Ravinet - Todos os direitos reservados.
      </div>
    </div>
  </div>

  <script>
    // Atualizar data e hora
    function atualizarDataHora() {
      const agora = new Date();
      const formatado = agora.toLocaleDateString('pt-BR') + ' ' + agora.toLocaleTimeString('pt-BR');
      document.getElementById('hora-data').innerText = formatado;
    }
    setInterval(atualizarDataHora, 1000);
    atualizarDataHora();

    // Botão WhatsApp
    document.getElementById("zap").href = "https://wa.me/551197346529?text=Olá%20gostaria%20de%20regularizar%20minha%20situação%20com%20a%20Ravinet";

    // Jogo dos balões
    let pontuacao = 0;
    let jogoIniciado = false;

    document.getElementById("jogarBtn").addEventListener("click", function () {
      if (jogoIniciado) return;
      jogoIniciado = true;

      document.getElementById("jogo").style.display = "block";
      const area = document.getElementById("gameArea");

      setInterval(() => {
        const balao = document.createElement("div");
        balao.className = "balao";
        const posX = Math.floor(Math.random() * 260);
        balao.style.left = posX + "px";
        balao.style.bottom = "0px";
        area.appendChild(balao);

        let posY = 0;
        const subir = setInterval(() => {
          posY += 2;
          balao.style.bottom = posY + "px";
          if (posY > 400) {
            clearInterval(subir);
            if (area.contains(balao)) area.removeChild(balao);
          }
        }, 20);

        balao.onclick = () => {
          clearInterval(subir);
          if (area.contains(balao)) area.removeChild(balao);
          pontuacao++;
          document.getElementById("score").innerText = "Pontuação: " + pontuacao;
        };
      }, 1000);
    });
  </script>
</body>
</html>
