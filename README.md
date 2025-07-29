# Cu
<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>電纜題庫練習</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 800px;
            margin: 20px auto;
            padding: 20px;
            background-color: #f4f4f4;
            color: #333;
        }
        h1 {
            text-align: center;
            color: #2c3e50;
        }
        .question {
            background-color: #fff;
            border: 1px solid #ddd;
            padding: 15px;
            margin-bottom: 20px;
            border-radius: 5px;
        }
        .question h3 {
            margin-top: 0;
            color: #34495e;
        }
        .option {
            margin: 10px 0;
        }
        .option input {
            margin-right: 10px;
        }
        button {
            display: block;
            margin: 20px auto;
            padding: 10px 20px;
            background-color: #3498db;
            color: #fff;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
        }
        button:hover {
            background-color: #2980b9;
        }
        #result {
            display: none;
            margin-top: 20px;
            padding: 15px;
            border-radius: 5px;
        }
        .correct {
            background-color: #dff0d8;
            border: 1px solid #3c763d;
            color: #3c763d;
        }
        .incorrect {
            background-color: #f2dede;
            border: 1px solid #a94442;
            color: #a94442;
        }
    </style>
</head>
<body>
    <h1>電纜題庫練習</h1>
    <div id="quiz">
        <!-- Questions will be inserted here by JavaScript -->
    </div>
    <button onclick="submitQuiz()">提交答案</button>
    <button onclick="resetQuiz()">重置測驗</button>
    <div id="result"></div>

    <script>
        const questions = [
            {
                question: "電纜何種結構具有防水功能",
                type: "single",
                options: ["包帶", "標蹤簇", "PE外被", "積層鋁帶"],
                correct: [2],
                explanation: "PE外被（聚乙烯外被）具有防水功能，是電纜中用於防止水分滲入的結構。"
            },
            {
                question: "彩色聚乙烯積層被覆電纜CCP-LAP-SS簡稱",
                type: "single",
                options: ["CCP電纜", "CLS電纜", "SS電纜", "LAP電纜"],
                correct: [1],
                explanation: "CCP-LAP-SS電纜的標準簡稱為CLS電纜。"
            },
            {
                question: "請問：同一材質電纜，何種線徑脈波傳播速度較快",
                type: "single",
                options: ["0.5mm", "0.9mm", "0.65mm", "0.4mm"],
                correct: [1],
                explanation: "同一材質電纜中，線徑較粗（如0.9mm）的脈波傳播速度較快，因其電阻較低，信號衰減較少。"
            },
            {
                question: "機房內存放充氣設備、局內外線分界",
                type: "single",
                options: ["電信機房", "人孔", "洞道", "大樓電信室"],
                correct: [2],
                explanation: "洞道是機房內存放充氣設備及作為局內外線分界的地方。"
            },
            {
                question: "以脈波反射儀量測障礙心線，斷路障礙其反射波形為",
                type: "single",
                options: ["無明顯波形", "向下突出之負脈波", "向上突出之正脈波", "先向下再向上突出之脈波"],
                correct: [2],
                explanation: "斷路障礙（開路）在脈波反射儀上會顯示向上突出的正脈波，因信號無法繼續傳導而反射。"
            },
            {
                question: "短路又稱自混，障礙代碼為",
                type: "single",
                options: ["VD", "DC", "MC", "SC"],
                correct: [3],
                explanation: "短路（自混）的障礙代碼為SC（Short Circuit）。"
            },
            {
                question: "屋內、外線路分界並具有防護雷擊的功能",
                type: "single",
                options: ["引接箱", "保安器", "接線盒", "電話機"],
                correct: [1],
                explanation: "保安器用於屋內外線路分界，並具有防護雷擊的功能。"
            },
            {
                question: "測試電容性線路，儀器螢光幕上波形為",
                type: "multiple",
                options: ["與斷線波形類似", "向上突出之正脈波", "向下突出之負脈波", "與短路波形類似"],
                correct: [2, 3],
                explanation: "測試電容性線路時，儀器螢光幕上波形為向下突出之負脈波，且與短路波形類似。"
            },
            {
                question: "10對芯線的電纜，黃白是第幾對",
                type: "single",
                options: ["第4對", "第1對", "第3對", "第2對"],
                correct: [2],
                explanation: "10對芯線電纜中，黃白為第3對，符合標準配色順序。"
            },
            {
                question: "電纜的理想被覆構造應具備",
                type: "single",
                options: ["價格高昂", "接續不易", "彎曲特特性良好", "愈重愈好"],
                correct: [2],
                explanation: "電纜的理想被覆構造應具有良好的彎曲特性，以適應安裝需求。"
            },
            {
                question: "混線又稱他混，障礙代碼為",
                type: "single",
                options: ["SC", "MC", "VD", "DC"],
                correct: [1],
                explanation: "混線（他混）的障礙代碼為MC（Mixed Circuit）。"
            },
            {
                question: "電纜內何種結構是用來分辨芯線順序",
                type: "single",
                options: ["PE外被", "包帶", "標蹤簇", "積層鋁帶"],
                correct: [2],
                explanation: "標蹤簇用於電纜內分辨芯線順序，通常以顏色或標記區分。"
            },
            {
                question: "交換局與交局間的連絡光纜稱",
                type: "single",
                options: ["客戶光纜", "分歧光纜", "中繼光纜", "主軸光纜"],
                correct: [2],
                explanation: "交換局與交局間的連絡光纜稱為中繼光纜。"
            },
            {
                question: "幹線電纜與配線電纜的分界",
                type: "single",
                options: ["分線箱", "大樓電信室", "引接箱", "交接箱"],
                correct: [3],
                explanation: "交接箱是幹線電纜與配線電纜的分界點。"
            },
            {
                question: "電橋法是以惠斯登平衡電橋為原理，發展應用有",
                type: "single",
                options: ["兩者皆非", "伐雷 (V法)測試法", "茂來(M法)測試法", "兩者皆是"],
                correct: [3],
                explanation: "電橋法基於惠斯登平衡電橋原理，包含伐雷(V法)和茂來(M法)測試法。"
            },
            {
                question: "目前地下幹線電纜使用何種絕緣",
                type: "single",
                options: ["紙帶", "FS", "PEF", "紙漿"],
                correct: [1],
                explanation: "目前地下幹線電纜多使用FS（發泡絕緣）作為絕緣材料。"
            },
            {
                question: "下列那一種電纜幾乎不再使用",
                type: "single",
                options: ["架空配線電纜", "地下幹線電纜", "中繼電纜", "地下配線電纜"],
                correct: [2],
                explanation: "中繼電纜因技術更新已幾乎不再使用。"
            },
            {
                question: "以脈波反射儀量測障礙心線，短路障礙其反射波形為",
                type: "single",
                options: ["向上突出之正脈波", "先向下再向上突出之脈波", "向下突出之負脈波", "無明顯波形"],
                correct: [2],
                explanation: "短路障礙在脈波反射儀上顯示向下突出的負脈波，因信號被短路點反射。"
            },
            {
                question: "測試電容性線路，線路有加感線圈，測試儀器螢光幕上波形為",
                type: "multiple",
                options: ["向下突出之負脈波", "與斷線波形類似", "向上突出之正脈波", "與短路波形類似"],
                correct: [1, 2],
                explanation: "加感線圈的電容性線路測試波形為向上突出之正脈波，且與斷線波形類似。"
            },
            {
                question: "電纜浸水障礙，測試儀器螢光幕上波形為",
                type: "single",
                options: ["向上突出之正脈波", "無法判斷", "類似雜音信號的脈波", "向下突出之負脈波"],
                correct: [2],
                explanation: "電纜浸水障礙會導致信號散亂，波形呈現類似雜音信號的脈波。"
            },
            {
                question: "下列何者不是電信網路三段式結構",
                type: "single",
                options: ["局外網路設備", "客戶終端設備", "以上皆非", "局內網路"],
                correct: [2],
                explanation: "電信網路三段式結構包含局內網路、局外網路設備、客戶終端設備，選項中「以上皆非」為正確答案。"
            },
            {
                question: "善用工具儀器可快速查測到障礙點，脈波反射法適用障礙類別有",
                type: "multiple",
                options: ["E", "DC", "MC", "SC"],
                correct: [1, 3],
                explanation: "脈波反射法適用於DC（斷路）和SC（短路）障礙類別。"
            },
            {
                question: "中華電信所使用的電纜芯線絞合方式",
                type: "single",
                options: ["對絞", "不絞", "星絞", "複絞"],
                correct: [2],
                explanation: "中華電信使用的電纜芯線絞合方式為星絞。"
            }
        ];

        function loadQuiz() {
            const quizDiv = document.getElementById('quiz');
            quizDiv.innerHTML = '';
            questions.forEach((q, index) => {
                const questionDiv = document.createElement('div');
                questionDiv.className = 'question';
                questionDiv.innerHTML = `<h3>${index + 1}. ${q.question}</h3>`;
                q.options.forEach((option, i) => {
                    const optionDiv = document.createElement('div');
                    optionDiv.className = 'option';
                    const inputType = q.type === 'multiple' ? 'checkbox' : 'radio';
                    optionDiv.innerHTML = `
                        <input type="${inputType}" name="q${index}" value="${i}">
                        ${option}
                    `;
                    questionDiv.appendChild(optionDiv);
                });
                quizDiv.appendChild(questionDiv);
            });
        }

        function submitQuiz() {
            let score = 0;
            const resultDiv = document.getElementById('result');
            resultDiv.innerHTML = '';
            questions.forEach((q, index) => {
                const selected = Array.from(document.querySelectorAll(`input[name="q${index}"]:checked`)).map(input => parseInt(input.value));
                const isCorrect = q.type === 'multiple' ?
                    selected.length === q.correct.length && selected.every(val => q.correct.includes(val)) :
                    selected.length === 1 && q.correct.includes(selected[0]);
                if (isCorrect) score++;
                const resultItem = document.createElement('div');
                resultItem.className = isCorrect ? 'correct' : 'incorrect';
                resultItem.innerHTML = `
                    <strong>題目 ${index + 1}: ${q.question}</strong><br>
                    您的答案: ${selected.length ? selected.map(i => q.options[i]).join(', ') : '未作答'}<br>
                    正確答案: ${q.correct.map(i => q.options[i]).join(', ')}<br>
                    說明: ${q.explanation}
                `;
                resultDiv.appendChild(resultItem);
            });
            resultDiv.innerHTML = `<h3>得分: ${score} / ${questions.length} (${(score / questions.length * 100).toFixed(2)}%)</h3>` + resultDiv.innerHTML;
            resultDiv.style.display = 'block';
        }

        function resetQuiz() {
            loadQuiz();
            document.getElementById('result').style.display = 'none';
        }

        // Load quiz on page load
        loadQuiz();
    </script>
</body>
</html>
