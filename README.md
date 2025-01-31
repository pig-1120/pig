<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <title>培養均衡飲食觀念:問答題</title>
    <style>
        body {
            background-color: #d3f4d3;
            font-family: Arial, sans-serif;
            text-align: center;
        }
        .container {
            margin: auto;
            width: 40%;
            padding: 20px;
            background-color: #ffffff;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        h1 {
            color: #006400; /* 深綠色 */
            font-size: 36px; /* 標題變大 */
        }
        .question {
            font-size: 18px; /* 與分數和時間相同大小 */
            margin-bottom: 10px; /* 縮小間距 */
        }
        .options {
            list-style-type: none;
            padding: 0;
        }
        .options li {
            margin: 10px 0; /* 縮小間距 */
            font-size: 18px; /* 與分數和時間相同大小 */
            background-color: #000000;
            color: #ffffff;
            padding: 10px;
            border-radius: 5px;
            cursor: pointer;
        }
        .options li:hover {
            background-color: #333333;
        }
        .result {
            font-size: 18px;
            margin-top: 10px; /* 縮小間距 */
            color: red;
        }
        .scoreboard, .timer {
            font-size: 18px;
            margin-bottom: 10px; /* 縮小間距 */
        }
        .restart {
            font-size: 18px;
            margin-top: 20px;
            cursor: pointer;
            color: blue;
            text-decoration: underline;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>培養均衡飲食觀念:問答題</h1>
        <div class="scoreboard">分數: <span id="score">0</span></div>
        <div class="timer">時間: <span id="time">0</span> 秒</div>
        <div class="question" id="question"></div>
        <ul class="options" id="options"></ul>
        <div class="result" id="result"></div>
        <div class="restart" id="restart" onclick="restartGame()">重新開始</div>
    </div>
    <script>
        const questions = [
            {
                question: "以下哪一種飲食方式最健康？",
                options: ["只吃肉類", "完全素食", "營養均衡的混合飲食", "以零食為主"],
                answer: 2,
                explanation: "營養均衡的混合飲食是最健康的選擇，因為它提供了多種營養素。"
            },
            // 其他9個問題
        ];

        let currentQuestion = 0;
        let score = 0;
        let time = 0;
        let timer;

        function startTimer() {
            timer = setInterval(() => {
                time++;
                document.getElementById('time').innerText = time;
            }, 1000);
        }

        function showQuestion() {
            if (currentQuestion < questions.length) {
                const q = questions[currentQuestion];
                document.getElementById('question').innerText = q.question;
                const options = document.getElementById('options');
                options.innerHTML = '';
                q.options.forEach((option, index) => {
                    const li = document.createElement('li');
                    li.innerText = option;
                    li.onclick = () => checkAnswer(index);
                    options.appendChild(li);
                });
            } else {
                endGame();
            }
        }

        function checkAnswer(index) {
            const q = questions[currentQuestion];
            const result = document.getElementById('result');
            if (index === q.answer) {
                score++;
                result.innerText = "答對了！" + q.explanation;
            } else {
                result.innerText = "答錯了。" + q.explanation;
            }
            document.getElementById('score').innerText = score;
            currentQuestion++;
            setTimeout(showQuestion, 2000);
        }

        function endGame() {
            clearInterval(timer);
            document.getElementById('question').innerText = "你好棒！恭喜你完成了";
            document.getElementById('options').innerHTML = '';
            document.getElementById('result').innerText = `總共使用時間: ${time} 秒，答對題數: ${score}，分數: ${score * 10}`;
            document.getElementById('restart').style.display = 'block';
        }

        function restartGame() {
            currentQuestion = 0;
            score = 0;
            time = 0;
            document.getElementById('score').innerText = score;
            document.getElementById('time').innerText = time;
            document.getElementById('result').innerText = '';
            document.getElementById('restart').style.display = 'none';
            startTimer();
            showQuestion();
        }

        window.onload = () => {
            startTimer();
            showQuestion();
        };
    </script>
</body>
</html>
