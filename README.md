# roleta-do-minecraft
joguem com seus amigos pra ver quem tem mais sorte
<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <title>Sorteio Minecraft Style</title>
    <style>
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background: #1a1a1a; color: white; text-align: center; padding: 20px; }
        .caixa-roleta { border: 4px solid #555; background: #333; padding: 30px; border-radius: 15px; display: inline-block; min-width: 300px; }
        .item-display { font-size: 2rem; margin: 20px 0; height: 60px; font-weight: bold; text-shadow: 2px 2px #000; }
        .pontos { font-size: 1.2rem; color: #ffcc00; margin-bottom: 20px; }
        button { padding: 15px 30px; font-size: 1.1rem; cursor: pointer; background: #3e8e41; color: white; border: none; border-radius: 5px; box-shadow: 0 4px #2e6631; }
        button:active { box-shadow: 0 0; transform: translateY(4px); }
        
        /* Cores das Raridades */
        .comum { color: #aaaaaa; }    /* Cinza */
        .raro { color: #55ff55; }     /* Verde */
        .epico { color: #55ffff; }    /* Ciano */
        .lendario { color: #ffaa00; } /* Laranja */
    </style>
</head>
<body>

    <h2>Bau de Recompensas Minecraft</h2>
    <div class="caixa-roleta">
        <div id="item-nome" class="item-display">Pronto?</div>
        <div id="item-pontos" class="pontos">Pontos: 0</div>
        <button onclick="girarRoleta()">ABRIR BAÚ</button>
    </div>

    <script>
        const itens = [
            { nome: "Terra", pontos: 1, raridade: "comum", peso: 60 },
            { nome: "Pedregulho", pontos: 1, raridade: "comum", peso: 60 },
            { nome: "Ferro", pontos: 5, raridade: "raro", peso: 25 },
            { nome: "Ouro", pontos: 5, raridade: "raro", peso: 20 },
            { nome: "Diamante", pontos: 25, raridade: "epico", peso: 10 },
            { nome: "Netherite", pontos: 100, raridade: "lendario", peso: 2 }
        ];

        function girarRoleta() {
            const btn = document.querySelector('button');
            btn.disabled = true;
            let giros = 0;
            
            // Efeito de "girando" antes de parar
            const intervalo = setInterval(() => {
                const aleatorio = itens[Math.floor(Math.random() * itens.length)];
                atualizarTela(aleatorio);
                giros++;
                
                if (giros > 15) {
                    clearInterval(intervalo);
                    resultadoFinal();
                    btn.disabled = false;
                }
            }, 100);
        }

        function resultadoFinal() {
            // Lógica de probabilidade baseada no peso
            const listaPesada = [];
            itens.forEach(item => {
                for (let i = 0; i < item.peso; i++) {
                    listaPesada.push(item);
                }
            });

            const resultado = listaPesada[Math.floor(Math.random() * listaPesada.length)];
            atualizarTela(resultado);
        }

        function atualizarTela(item) {
            const display = document.getElementById('item-nome');
            display.innerText = item.nome;
            display.className = "item-display " + item.raridade;
            document.getElementById('item-pontos').innerText = "Pontos: " + item.pontos;
        }
    </script>
</body>
</html>
