<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Save the Date - Contagem Regressiva</title>
    <style>
        /* As fontes originais */
        @import url('https://fonts.googleapis.com/css2?family=Roboto+Mono:wght@700&family=Roboto:wght@500&display=swap');

        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background-color: #f0f0f0;
            /* Adicionado para evitar overflow em telas muito pequenas */
            padding: 10px;
            box-sizing: border-box;
        }

        .background-container {
            position: relative;
            
            /* O QUE MUDOU (PARTE 1): A base da responsividade */
            width: 100%;             /* Ocupa 100% do espaço disponível no body */
            max-width: 1280px;       /* Mas não ultrapassa a largura original da imagem */
            aspect-ratio: 1280 / 1020; /* Força o container a MANTER a proporção da imagem (largura/altura) */

            background-image: url('save_the_data.jpeg');
            background-size: contain;
            background-repeat: no-repeat;
            background-position: center;
        }

        .countdown-container {
            position: absolute;

            /* O QUE MUDOU (PARTE 2): A largura agora é relativa */
            width: 39%; /* 500px é aproximadamente 39% de 1280px. Assim a largura diminui com o container */

            text-align: center;
            
            /* As posições percentuais originais agora funcionam, pois são relativas ao container que está escalando corretamente! */
            top: 46.5%;
            left: 28.5%;
            transform: translate(-40%, -50%);
        }

        .title {
            /* A fonte "Spline Sans Medium" não estava importada, voltei para a família Roboto para garantir consistência */
            font-family: 'Roboto', sans-serif;
            color: #444;
            letter-spacing: 0.1rem;
            margin-bottom: 5px;
            font-weight: 400;

            /* O QUE MUDOU (PARTE 3): Fonte fluida */
            font-size: clamp(0.5rem, 1.5vw, 1.0rem); /* Mínimo, Preferencial (escala com a tela), Máximo */
        }

        .timer {
            display: flex;
            justify-content: center;
            /* O QUE MUDOU (PARTE 3): Espaçamento fluido */
            gap: clamp(5px, 2vw, 20px);
        }

        .time-box {
            display: flex;
            flex-direction: column;
            align-items: center;
            min-width: 0; /* Removido o min-width fixo para permitir que encolha */
        }

        .time-value {
            font-family: 'Roboto Mono', monospace;
            font-weight: 700;
            color: #000;
            
            /* O QUE MUDOU (PARTE 3): Fonte gigante fluida */
            font-size: clamp(1.5rem, 5.5vw, 3.7rem); /* Mínimo, Preferencial, Máximo */
        }

        .time-label {
            font-family: 'Roboto', sans-serif;
            font-weight: 500;
            color: #333;
            margin-top: 2px;
            
            /* O QUE MUDOU (PARTE 3): Fonte fluida */
            font-size: clamp(0.5rem, 1.2vw, 0.8rem);
        }
    </style>
</head>
<body>

    <div class="background-container">
        <div class="countdown-container">
            <div class="title"><strong>Contagem regressiva começou </strong> ⏳</div>
            <div class="timer" id="timer">
                <div class="time-box">
                    <div id="days" class="time-value">00</div>
                    <div class="time-label">DIAS</div>
                </div>
                <div class="time-box">
                    <div id="hours" class="time-value">00</div>
                    <div class="time-label">HORAS</div>
                </div>
                <div class="time-box">
                    <div id="minutes" class="time-value">00</div>
                    <div class="time-label">MINUTOS</div>
                </div>
                <div class="time-box">
                    <div id="seconds" class="time-value">00</div>
                    <div class="time-label">SEGUNDOS</div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // SEU JAVASCRIPT ORIGINAL ESTÁ PERFEITO E NÃO PRECISA DE MUDANÇAS.
        const countdown = () => {
            const eventDate = new Date('2025-08-18T00:00:00').getTime();
            const now = new Date().getTime();
            const gap = eventDate - now;
            if (gap < 0) {
                clearInterval(countdownInterval);
                document.querySelector('.timer').innerHTML = "<h2 style='color:black;'>O EVENTO COMEÇOU!</h2>";
                document.querySelector('.title').style.display = 'none';
                return;
            }
            const second = 1000;
            const minute = second * 60;
            const hour = minute * 60;
            const day = hour * 24;
            const textDay = Math.floor(gap / day);
            const textHour = Math.floor((gap % day) / hour);
            const textMinute = Math.floor((gap % hour) / minute);
            const textSecond = Math.floor((gap % minute) / second);
            const formatTime = (time) => (time < 10 ? `0${time}` : time);
            document.getElementById('days').innerText = formatTime(textDay);
            document.getElementById('hours').innerText = formatTime(textHour);
            document.getElementById('minutes').innerText = formatTime(textMinute);
            document.getElementById('seconds').innerText = formatTime(textSecond);
        };
        const countdownInterval = setInterval(countdown, 1000);
        countdown();
    </script>

</body>
</html>
