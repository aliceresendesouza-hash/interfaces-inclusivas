<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Desafio: Estabilidade de Leitura</title>
  
  <style>
    /* ==========================================================================
       1. RESET E CONFIGURAÇÕES VISUAIS
       ========================================================================== */
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background-color: #f4f6f9;
      color: #333;
      display: flex;
      flex-direction: column;
      align-items: center;
      padding: 40px 20px;
    }

    .container {
      max-width: 500px;
      width: 100%;
      background: white;
      padding: 30px;
      border-radius: 12px;
      box-shadow: 0 4px 15px rgba(0,0,0,0.05);
      text-align: center;
    }

    h1 {
      font-size: 1.8rem;
      color: #2c3e50;
      margin-bottom: 10px;
    }

    p {
      color: #7f8c8d;
      margin-bottom: 20px;
      font-size: 0.95rem;
    }

    /* ==========================================================================
       2. BOTÃO E ANIMAÇÃO (INTERAÇÕES)
       ========================================================================== */
    .btn-leitura {
      background-color: #3498db;
      color: white;
      border: none;
      padding: 12px 24px;
      font-size: 1rem;
      font-weight: bold;
      border-radius: 8px;
      cursor: pointer;
      transition: all 0.2s;
      width: 100%;
    }

    .btn-leitura:hover {
      background-color: #2980b9;
    }

    /* Estado desabilitado quando a leitura já estiver acontecendo */
    .btn-leitura:disabled {
      background-color: #bdc3c7;
      cursor: not-allowed;
      transform: none;
    }

    .status-painel {
      margin-top: 25px;
      padding: 15px;
      background-color: #f8f9fa;
      border-left: 4px solid #3498db;
      border-radius: 4px;
      text-align: left;
      min-height: 80px;
    }

    .loading {
      color: #e67e22;
      font-weight: bold;
    }

    .sucesso {
      color: #2ecc71;
      font-weight: bold;
    }
  </style>
</head>
<body>

  <div class="container">
    <h1>Controle de Fluxo de Leitura</h1>
    <p>Clique no botão repetidamente para testar a estabilidade. O sistema impede leituras duplicadas em paralelo.</p>

    <button id="btnIniciar" class="btn-leitura">Iniciar Leitura de Dados</button>

    <div class="status-painel">
      <div id="logStatus">Sistema pronto. Aguardando comando...</div>
    </div>
  </div>

  <script>
    const btnIniciar = document.getElementById('btnIniciar');
    const logStatus = document.getElementById('logStatus');
    
    // Variável de estado que impede a execução simultânea
    let leituraEmAndamento = false;
    let timeoutId = null;

    btnIniciar.addEventListener('click', () => {
      
      // 1. Se já houver uma leitura rodando, interrompe e reseta o temporizador anterior
      if (leituraEmAndamento) {
        clearTimeout(timeoutId);
        logStatus.innerHTML = '<span class="loading">Leitura anterior cancelada! Reiniciando processo...</span>';
      }

      // 2. Define que o processo começou
      leituraEmAndamento = true;
      btnIniciar.innerText = "Carregando...";
      
      if (!timeoutId) {
        logStatus.innerHTML = '<span class="loading">Buscando informações no banco de dados...</span>';
      }

      // Simula uma resposta assíncrona/leitura que demora 2 segundos
      timeoutId = setTimeout(() => {
        
        // 3. Finaliza com sucesso e libera o estado para novas leituras
        logStatus.innerHTML = `
          <span class="sucesso">✓ Leitura concluída com sucesso!</span><br>
          <small>Dados processados de forma estável às ${new Date().toLocaleTimeString()}.</small>
        `;
        
        // Reseta os controladores
        leituraEmAndamento = false;
        timeoutId = null;
        btnIniciar.innerText = "Iniciar Leitura de Dados";

      }, 2000); 
    });
  </script>

</body>
</html># interfaces-inclusivas
