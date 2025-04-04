<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>🔥 แบบทดสอบความรู้ทั่วไป 🔥</title>

    <!-- ใช้ฟ้อนต์พิเศษจาก Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&family=Poppins:wght@500&display=swap" rel="stylesheet">

    <style>
        body {
            background: linear-gradient(45deg, #00c6ff, #0072ff, #00b7ff); /* โทนเย็น ฟ้าสด */
            background-size: 400% 400%;
            animation: gradientAnimation 10s ease infinite;
            font-family: 'Poppins', sans-serif;
            color: white;
            text-align: center;
            margin: 0;
            padding: 0;
        }

        /* การเคลื่อนไหวของพื้นหลัง */
        @keyframes gradientAnimation {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        h1 {
            font-size: 40px;
            color: #fff;
            margin-top: 20px;
            font-family: 'Roboto', sans-serif;
        }

        .quiz-container {
            background-color: rgba(0, 0, 0, 0.7);
            padding: 20px;
            border-radius: 10px;
            display: inline-block;
            box-shadow: 0 0 15px #00b7ff;
            width: 300px;
            transition: transform 0.3s ease-in-out;
        }

        .quiz-container:hover {
            transform: scale(1.05);
        }

        .option-btn {
            background-color: #444;
            color: white;
            border: none;
            padding: 20px;
            margin: 5px;
            width: 100%;
            height: 60px;
            cursor: pointer;
            border-radius: 5px;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            justify-content: center;
            text-align: center;
        }

        .option-btn:hover {
            background-color: #00b7ff;
        }

        .selected {
            background-color: #00b7ff !important;
        }

        .hidden {
            display: none;
        }

        #result {
            color: #FFD700;
            font-size: 36px;
            margin-top: 20px;
            font-weight: bold;
            text-transform: uppercase;
            letter-spacing: 2px;
            text-shadow: 0 0 15px #00b7ff, 0 0 30px #00b7ff, 0 0 45px #00b7ff;
            opacity: 0;
            animation: resultFadeIn 1s forwards;
        }

        /* การเคลื่อนไหวของผลลัพธ์ */
        @keyframes resultFadeIn {
            0% { opacity: 0; transform: translateY(30px); }
            100% { opacity: 1; transform: translateY(0); }
        }

        /* ปุ่มให้กลับไปทำแบบทดสอบใหม่ */
        button {
            padding: 15px 30px;
            background-color: #00b7ff;
            border: none;
            color: white;
            font-size: 20px;
            margin-top: 20px;
            border-radius: 10px;
            cursor: pointer;
            box-shadow: 0 0 10px #00b7ff;
            transition: all 0.3s ease;
        }

        button:hover {
            background-color: #00c6ff;
            transform: scale(1.1);
        }

        /* สีเขียวเรืองแสงสำหรับผลสอบติด */
        .pass {
            color: #00FF00;
            text-shadow: 0 0 15px #00FF00, 0 0 30px #00FF00, 0 0 45px #00FF00;
        }

        /* สีแดงเรืองแสงสำหรับสอบไม่ติด */
        .fail {
            color: #FF0000;
            text-shadow: 0 0 15px #FF0000, 0 0 30px #FF0000, 0 0 45px #FF0000;
        }

    </style>
</head>
<body>

    <h1>🔥 ร้อนวิชา 🔥</h1>
    <h1>  คอมพิวเตอร์ </h1>
    <div class="quiz-container">
        <h2 id="question">Loading...</h2>
        <div id="options"></div>
        <p>⏳ เวลาที่เหลือ: <span id="timer">15</span> วินาที</p>
        <button id="next-btn" class="hidden">ถัดไป →</button>
    </div>
    <p id="result" class="hidden"></p>

    <script>
        const quizData = [
            { question: "เมืองหลวงของประเทศไทยคือ?", options: ["เชียงใหม่", "กรุงเทพฯ", "ขอนแก่น", "ภูเก็ต"], correctAnswer: "กรุงเทพฯ" },
            { question: "2 + 2 เท่ากับ?", options: ["3", "4", "5", "6"], correctAnswer: "4" },
            { question: "สัตว์ชนิดใดเป็นสัตว์เลี้ยงลูกด้วยนม?", options: ["จระเข้", "เพนกวิน", "วาฬ", "งู"], correctAnswer: "วาฬ" },
            { question: "น้ำเดือดที่อุณหภูมิเท่าไหร่?", options: ["50°C", "75°C", "100°C", "120°C"], correctAnswer: "100°C" },
            { question: "สัตว์ชนิดใดมีชีวิตในน้ำ?", options: ["สิงโต", "ปลา", "ช้าง", "นก"], correctAnswer: "ปลา" }
        ];

        let currentQuestion = 0;
        let score = 0;
        let selectedAnswer = null;
        let timer = 15;
        let timerInterval;

        const questionElement = document.getElementById("question");
        const optionsElement = document.getElementById("options");
        const timerElement = document.getElementById("timer");
        const nextButton = document.getElementById("next-btn");
        const resultElement = document.getElementById("result");

        function startTimer() {
            timer = 15;
            timerElement.innerText = timer;
            clearInterval(timerInterval);
            timerInterval = setInterval(() => {
                timer--;
                timerElement.innerText = timer;
                if (timer === 0) {
                    clearInterval(timerInterval);
                    handleNextQuestion();
                }
            }, 1000);
        }

        function loadQuestion() {
            if (currentQuestion >= quizData.length) {
                showResult();
                return;
            }
            const q = quizData[currentQuestion];
            questionElement.innerText = q.question;
            optionsElement.innerHTML = "";
            q.options.forEach(option => {
                const btn = document.createElement("button");
                btn.innerText = option;
                btn.classList.add("option-btn");
                btn.onclick = () => {
                    document.querySelectorAll(".option-btn").forEach(btn => btn.classList.remove("selected"));
                    btn.classList.add("selected");
                    selectedAnswer = option;
                    nextButton.classList.remove("hidden");
                    nextButton.classList.add("fade-in");
                };
                optionsElement.appendChild(btn);
            });
            nextButton.classList.add("hidden");
            startTimer();
        }

        function handleNextQuestion() {
            clearInterval(timerInterval);
            if (selectedAnswer === quizData[currentQuestion].correctAnswer) {
                score++;
            }
            currentQuestion++;
            selectedAnswer = null;
            loadQuestion();
        }

        function showResult() {
            document.querySelector(".quiz-container").classList.add("hidden");
            const percentage = (score / quizData.length) * 100;
            let resultMessage = "";
            let resultClass = "";
            
            if (percentage >= 60) {
                resultMessage = "🎉 คุณสอบติด 🎉";
                resultClass = "pass";
            } else {
                resultMessage = "❌ สอบไม่ติด ❌";
                resultClass = "fail";
            }

            resultElement.innerHTML = `<h2 class="fade-in ${resultClass}">${resultMessage}</h2>
                                       <p class="fade-in">คุณได้คะแนน <strong>${score} / ${quizData.length}</strong></p>
                                       <button onclick="location.reload()" class="fade-in">🔄 ทำแบบทดสอบอีกครั้ง</button>`;
            resultElement.classList.remove("hidden");
        }

        nextButton.onclick = handleNextQuestion;

        // เมื่อโหลดหน้าเว็บให้เริ่มคำถามแรกทันที
        window.onload = loadQuestion;
    </script>

</body>
</html>
