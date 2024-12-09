<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>لعبة الليمون</title>
    <style>
        body {
            margin: 0;
            padding: 0;
            background-color: #556b2f; /* Olive green color */
            font-family: 'Arial', sans-serif;
            overflow: hidden;
        }
        header {
            background-color: #6b8e23; /* Dark olive green */
            color: white;
            padding: 20px;
            text-align: center;
            font-size: 1.5em;
        }
        .score {
            position: fixed;
            top: 20px;
            left: 20px;
            background: #8fbc8f; /* Light olive */
            color: #fff;
            padding: 10px;
            border-radius: 10px;
            font-size: 1.2em;
        }
        .lemon {
            position: absolute;
            width: 50px;
            height: 50px;
            background: url('https://i.ibb.co/0GLFPjx/028be632-fc66-4e18-aa29-933c44a04d65.webp') no-repeat center;
            background-size: cover;
            cursor: pointer;
        }
        .start-button {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background-color: #8fbc8f;
            color: white;
            padding: 15px 30px;
            border: none;
            border-radius: 5px;
            font-size: 1.5em;
            cursor: pointer;
        }
        .start-button:hover {
            background-color: #6b8e23;
        }
        .message {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: rgba(255, 255, 255, 0.9);
            padding: 30px;
            border-radius: 10px;
            text-align: center;
            display: none;
            font-size: 1.5em;
            color: #556b2f;
        }
    </style>
</head>
<body>
    <header>
        اجمع الليمون 🍋
    </header>
    <div class="score">النقاط: 0</div>
    <button class="start-button" onclick="startGame()">ابدأ اللعبة</button>
    <div class="message" id="win-message">
        🎉 لقد جمعت 21 ليمونة! <br> أحبك ليمون ❤️
    </div>

    <script>
        let score = 0;
        let gameStarted = false;

        function startGame() {
            if (!gameStarted) {
                gameStarted = true;
                document.querySelector(".start-button").style.display = "none";
                createLemon();
            }
        }

        function createLemon() {
            const lemon = document.createElement("div");
            lemon.classList.add("lemon");

            // Generate random positions within the viewport
            const x = Math.random() * (window.innerWidth - 50);
            const y = Math.random() * (window.innerHeight - 50);

            lemon.style.left = `${x}px`;
            lemon.style.top = `${y}px`;

            // Add click event to increase score and remove lemon
            lemon.addEventListener("click", () => {
                score++;
                document.querySelector(".score").textContent = `النقاط: ${score}`;
                lemon.remove();
                if (score === 21) {
                    displayWinMessage();
                } else {
                    createLemon(); // Create a new lemon after clicking
                }
            });

            // Append lemon to the body
            document.body.appendChild(lemon);

            // Remove the lemon after 3 seconds if not clicked and create a new one
            setTimeout(() => {
                if (document.body.contains(lemon)) {
                    lemon.remove();
                    if (gameStarted) createLemon();
                }
            }, 3000);
        }

        function displayWinMessage() {
            const message = document.getElementById("win-message");
            message.style.display = "block";
        }
    </script>
</body>
</html>
