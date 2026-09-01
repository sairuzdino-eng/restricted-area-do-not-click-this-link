<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>restricted area do not click this link</title>
    <style>
        :root {
            --bg-dark: #12091f;
            --bg-purple: #23113b;
            --accent-pink: #ff79c6;
            --accent-purple: #9b51e0;
            --text-light: #f8f8f2;
            --card-bg: rgba(35, 17, 59, 0.85);
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            background: radial-gradient(circle at center, var(--bg-purple), var(--bg-dark));
            color: var(--text-light);
            overflow: hidden;
            position: relative;
        }

        /* Floating background elements */
        .bg-heart {
            position: absolute;
            color: var(--accent-pink);
            opacity: 0.25;
            animation: floatAnim 6s infinite ease-in-out;
            user-select: none;
            pointer-events: none;
            z-index: 1;
        }

        @keyframes floatAnim {
            0%, 100% { transform: translateY(0) rotate(0deg); }
            50% { transform: translateY(-25px) rotate(12deg); }
        }

        /* Main Card Container */
        .card-container {
            position: relative;
            z-index: 10;
            background: var(--card-bg);
            padding: 2.5rem 2rem;
            border-radius: 24px;
            border: 2px solid var(--accent-pink);
            box-shadow: 0 0 35px rgba(155, 81, 224, 0.45), inset 0 0 15px rgba(255, 121, 198, 0.2);
            backdrop-filter: blur(12px);
            text-align: center;
            max-width: 420px;
            width: 90%;
        }

        .kuromi-tag {
            display: inline-block;
            background: var(--accent-purple);
            color: #ffffff;
            padding: 6px 14px;
            border-radius: 20px;
            font-size: 0.75rem;
            font-weight: 700;
            letter-spacing: 1.5px;
            margin-bottom: 1.2rem;
            text-transform: uppercase;
            box-shadow: 0 2px 10px rgba(155, 81, 224, 0.4);
        }

        h1 {
            font-size: 1.8rem;
            color: #ffffff;
            margin-bottom: 0.5rem;
            text-shadow: 0 0 12px var(--accent-pink);
        }

        .date-text {
            color: var(--accent-pink);
            font-size: 1.1rem;
            font-weight: 600;
            margin-bottom: 1.2rem;
        }

        .message-text {
            font-size: 0.95rem;
            color: #e0d0f0;
            margin-bottom: 2rem;
            line-height: 1.5;
        }

        .button-zone {
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 1.5rem;
            min-height: 60px;
            position: relative;
        }

        button {
            padding: 12px 28px;
            font-size: 1rem;
            font-weight: 700;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            transition: transform 0.2s cubic-bezier(0.175, 0.885, 0.32, 1.275), box-shadow 0.2s ease;
        }

        .btn-yes {
            background: linear-gradient(45deg, var(--accent-pink), var(--accent-purple));
            color: #ffffff;
            box-shadow: 0 4px 15px rgba(255, 121, 198, 0.5);
            z-index: 12;
        }

        .btn-yes:hover {
            box-shadow: 0 6px 22px rgba(255, 121, 198, 0.8);
        }

        .btn-no {
            background: rgba(255, 255, 255, 0.08);
            color: #d1c4e9;
            border: 1px solid rgba(255, 255, 255, 0.2);
            z-index: 11;
        }

        .alert-message {
            min-height: 28px;
            margin-top: 1.5rem;
            font-size: 0.88rem;
            color: var(--accent-pink);
            font-weight: 700;
            letter-spacing: 0.5px;
            text-shadow: 0 0 8px rgba(255, 121, 198, 0.6);
        }

        /* Success Overlay */
        .overlay {
            display: none;
            position: fixed;
            top: 0; left: 0; right: 0; bottom: 0;
            background: rgba(18, 9, 31, 0.96);
            z-index: 100;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            padding: 2rem;
        }

        .overlay h2 {
            font-size: 2.4rem;
            color: var(--accent-pink);
            margin-bottom: 1rem;
            text-shadow: 0 0 18px var(--accent-pink);
        }

        .overlay p {
            font-size: 1.15rem;
            color: #ffffff;
            max-width: 380px;
            line-height: 1.4;
        }
    </style>
</head>
<body>

    <div class="bg-heart" style="top: 12%; left: 12%; font-size: 22px;">🖤</div>
    <div class="bg-heart" style="top: 22%; left: 82%; font-size: 28px;">💜</div>
    <div class="bg-heart" style="top: 72%; left: 15%; font-size: 24px;">💀</div>
    <div class="bg-heart" style="top: 82%; left: 78%; font-size: 20px;">✨</div>

    <div class="card-container">
        <div class="kuromi-tag">Top Secret Notice</div>
        <h1>Movie Date? 🎬</h1>
        <p class="date-text">September 02, 2026 ✨</p>
        <p class="message-text">Since it's your special day, I'd love to take you out to celebrate your birthday with a movie date!</p>

        <div class="button-zone">
            <button class="btn-yes" id="yesBtn" onclick="onYesClick()">YES! 💜</button>
            <button class="btn-no" id="noBtn" onclick="onNoClick()">No</button>
        </div>

        <div class="alert-message" id="alertBox"></div>
    </div>

    <div class="overlay" id="successOverlay">
        <h2>It's a Date! 🖤✨</h2>
        <p>Happy Birthday! Get ready for September 2nd, 2026. 🎂🍿</p>
    </div>

    <script>
        let clickCounter = 0;
        const noButton = document.getElementById('noBtn');
        const yesButton = document.getElementById('yesBtn');
        const alertBox = document.getElementById('alertBox');

        const promptMessages = [
            "Please click YES! 🥺",
            "Error: 'No' is strictly disabled. Click YES! 💜",
            "Nice try, but you have to click YES! ✨",
            "Kuromi says: Click YES right now! 💀",
            "Seriously, click YES! 🖤"
        ];

        function onNoClick() {
            // Display progressive pleading messages
            alertBox.innerText = promptMessages[clickCounter % promptMessages.length];
            clickCounter++;

            // Incrementally grow the YES button to make clicking YES easier
            let currentScale = 1 + (clickCounter * 0.18);
            yesButton.style.transform = scale(${currentScale});

            // Teleport the NO button randomly across the viewport
            const padding = 50;
            const maxX = window.innerWidth - noButton.offsetWidth - padding;
            const maxY = window.innerHeight - noButton.offsetHeight - padding;

            const randomX = Math.max(padding, Math.floor(Math.random() * maxX));
            const randomY = Math.max(padding, Math.floor(Math.random() * maxY));

            noButton.style.position = 'fixed';
            noButton.style.left = ${randomX}px;
            noButton.style.top = ${randomY}px;
        }

        function onYesClick() {
            document.getElementById('successOverlay').style.display = 'flex';
        }
    </script>
</body>
</html>
