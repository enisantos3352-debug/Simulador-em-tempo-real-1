
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Matrix - Centro & Média (BTC)</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: #0b0e11;
            color: #d1d4dc;
            margin: 0;
            padding: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        .container {
            width: 100%;
            max-width: 500px;
            background: #1e222d;
            border: 1px solid #2a2e39;
            border-radius: 8px;
            padding: 20px;
            box-sizing: border-box;
            box-shadow: 0 4px 12px rgba(0,0,0,0.4);
        }
        h2 {
            color: #3861fb;
            font-size: 17px;
            text-align: center;
            margin-top: 0;
            margin-bottom: 15px;
            letter-spacing: 1px;
        }
        .live-card {
            background: #131722;
            padding: 12px;
            border-radius: 6px;
            text-align: center;
            margin-bottom: 12px;
            border: 1px solid #2a2e39;
        }
        .live-label {
            font-size: 11px;
            color: #848e9c;
            text-transform: uppercase;
        }
        .live-value {
            font-size: 22px;
            font-weight: bold;
            color: #f3ba2f;
            margin-top: 3px;
        }
        .grid-stats {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
            margin-bottom: 12px;
        }
        .stat-box {
            background: #131722;
            padding: 10px;
            border-radius: 6px;
            text-align: center;
            border: 1px solid #2a2e39;
        }
        .stat-label {
            font-size: 10px;
            color: #848e9c;
            margin-bottom: 3px;
            text-transform: uppercase;
        }
        .stat-val-max { font-size: 14px; font-weight: bold; color: #2ebd85; }
        .stat-val-min { font-size: 14px; font-weight: bold; color: #f6465d; }
        
        .center-card {
            background: #131722;
            padding: 12px;
            border-radius: 6px;
            text-align: center;
            border: 1px solid #3861fb;
            margin-bottom: 12px;
        }
        .center-label { font-size: 11px; color: #3861fb; font-weight: bold; text-transform: uppercase; }
        .center-value { font-size: 20px; font-weight: bold; color: #ffffff; margin-top: 3px; }

        .ma-card {
            background: #131722;
            padding: 12px;
            border-radius: 6px;
            text-align: center;
            border: 1px solid #f3ba2f;
            margin-bottom: 12px;
        }
        .ma-label { font-size: 11px; color: #f3ba2f; font-weight: bold; text-transform: uppercase; }
        .ma-value { font-size: 20px; font-weight: bold; color: #ffffff; margin-top: 3px; }

        .signal-box {
            padding: 12px;
            border-radius: 6px;
            text-align: center;
            font-weight: bold;
            font-size: 13px;
            background: #131722;
            border: 1px solid #2a2e39;
        }
        .signal-buy { background: #005c29; color: #fff; border-color: #2ebd85; }
        .signal-sell { background: #7a1c2a; color: #fff; border-color: #f6465d; }
        .signal-wait { color: #848e9c; }

        /* Tela de Bloqueio com o Pix */
        #tela-bloqueio {
            display: none;
            background: #131722;
            border: 2px solid #f6465d;
            border-radius: 8px;
            padding: 20px;
            text-align: center;
        }
        #tela-bloqueio h3 { color: #f6465d; margin-top: 0; }
        .pix-box {
            background: #1e222d;
            border: 1px dashed #2ebd85;
            padding: 12px;
            border-radius: 6px;
            margin: 12px 0;
        }
        .pix-chave {
            font-size: 16px;
            font-weight: bold;
            color: #2ebd85;
            margin-top: 5px;
            word-break: break-all;
        }
        .btn-whatsapp {
            display: inline-block;
            margin-top: 10px;
            background: #25d366;
            color: #fff;
            padding: 12px 18px;
            border-radius: 6px;
            text-decoration: none;
            font-weight: bold;
            font-size: 14px;
        }

        .footer-info {
            font-size: 10px;
            color: #787b86;
            text-align: center;
            margin-top: 12px;
        }
    </style>
</head>
<body>

    <div class="container">
        <h2>Matrix - Centro & Média (BTC)</h2>
        
        <!-- PAINEL PRINCIPAL -->
        <div id="painel-principal">
            <div class="live-card">
                <div class="live-label">Preço Atual ao Vivo</div>
                <div class="live-value" id="preco-atual">Carregando...</div>
            </div>

            <div class="grid-stats">
                <div class="stat-box">
                    <div class="stat-label">Máxima (24h)</div>
                    <div class="stat-val-max" id="preco-max">--</div>
                </div>
                <div class="stat-box">
                    <div class="stat-label">Mínima (24h)</div>
                    <div class="stat-val-min" id="preco-min">--</div>
                </div>
            </div>

            <div class="center-card">
                <div class="center-label">Preço Central (Máx + Mín / 2)</div>
                <div class="center-value" id="preco-centro">--</div>
            </div>

            <div class="ma-card">
                <div class="ma-label">Média Móvel (Rápida)</div>
                <div class="ma-value" id="preco-ma">--</div>
            </div>

            <div id="sinal-cruzamento" class="signal-box signal-wait">
                Aguardando cruzamento da Média com o Centro...
            </div>
        </div>

        <!-- TELA DE BLOQUEIO COM PIX -->
        <div id="tela-bloqueio">
            <h3>⏰ Período de Teste Expirado!</h3>
            <p style="font-size: 13px; color: #d1d4dc;">Seu teste gratuito de 3 dias acabou. Para renovar por <strong>R$ 25/mês</strong>, faça o Pix para a chave abaixo:</p>
            
            <div class="pix-box">
                <div style="font-size: 11px; color: #848e9c; text-transform: uppercase;">Chave Pix (Telefone)</div>
                <div class="pix-chave">92985966939</div>
                <div style="font-size: 11px; color: #d1d4dc; margin-top: 5px;">Valor: <strong>R$ 25,00</strong></div>
            </div>

            <p style="font-size: 12px; color: #848e9c;">Assim que fizer o pagamento, mande o comprovante para o WhatsApp abaixo:</p>
            
            <a href="https://wa.me/5585992704001?text=Olá!%20Acabei%20de%20fazer%20o%20Pix%20de%20R$%2025%20para%20renovar%20o%20simulador.%20Segue%20o%20comprovante." target="_blank" class="btn-whatsapp">Mandar Comprovante no WhatsApp</a>
        </div>

        <div class="footer-info">Sistema de Teste Gratuito - 3 Dias</div>
    </div>

    <script>
        function verificarValidadeTeste() {
            const diasDeTeste = 3;
            const msPorDia = 24 * 60 * 60 * 1000;
            
            let dataInicio = localStorage.getItem('matrix_inicio_teste');
            
            if (!dataInicio) {
                dataInicio = new Date().getTime();
                localStorage.setItem('matrix_inicio_teste', dataInicio);
            }

            let agora = new Date().getTime();
            let tempoDecorrido = agora - parseInt(dataInicio);
            let limiteTeste = diasDeTeste * msPorDia;

            if (tempoDecorrido > limiteTeste) {
                document.getElementById('painel-principal').style.display = 'none';
                document.getElementById('tela-bloqueio').style.display = 'block';
                return false;
            }
            return true;
        }

        let historicoPrecos = [];

        async function monitorarMatrixComMA() {
            if (!verificarValidadeTeste()) return;

            try {
                const res = await fetch('https://api.binance.com/api/v3/ticker/24hr?symbol=BTCUSDT');
                const data = await res.json();

                const precoAtual = parseFloat(data.lastPrice);
                const maxDia = parseFloat(data.highPrice);
                const minDia = parseFloat(data.lowPrice);

                const precoCentro = (maxDia + minDia) / 2;

                historicoPrecos.push(precoAtual);
                if (historicoPrecos.length > 5) {
                    historicoPrecos.shift();
                }

                let soma = historicoPrecos.reduce((a, b) => a + b, 0);
                let mediaMovel = soma / historicoPrecos.length;

                document.getElementById('preco-atual').innerText = `$ ${precoAtual.toLocaleString('en-US', {minimumFractionDigits: 2, maximumFractionDigits: 2})}`;
                document.getElementById('preco-max').innerText = `$ ${maxDia.toLocaleString('en-US', {minimumFractionDigits: 2, maximumFractionDigits: 2})}`;
                document.getElementById('preco-min').innerText = `$ ${minDia.toLocaleString('en-US', {minimumFractionDigits: 2, maximumFractionDigits: 2})}`;
                document.getElementById('preco-centro').innerText = `$ ${precoCentro.toLocaleString('en-US', {minimumFractionDigits: 2, maximumFractionDigits: 2})}`;
                document.getElementById('preco-ma').innerText = `$ ${mediaMovel.toLocaleString('en-US', {minimumFractionDigits: 2, maximumFractionDigits: 2})}`;

                let caixaSinal = document.getElementById('sinal-cruzamento');
                if (mediaMovel > precoCentro) {
                    caixaSinal.className = 'signal-box signal-buy';
                    caixaSinal.innerHTML = '🚀 SINAL DE COMPRA<br>Média Acima do Preço Central!';
                } else if (mediaMovel < precoCentro) {
                    caixaSinal.className = 'signal-box signal-sell';
                    caixaSinal.innerHTML = '📉 SINAL DE VENDA<br>Média Abaixo do Preço Central!';
                } else {
                    caixaSinal.className = 'signal-box signal-wait';
                    caixaSinal.innerText = 'Preço alinhado no Centro';
                }

            } catch (e) {
                console.error("Erro ao buscar dados:", e);
            }
        }

        if (verificarValidadeTeste()) {
            setInterval(monitorarMatrixComMA, 2000);
            monitorarMatrixComMA();
        }
    </script>

</body>
</html>
