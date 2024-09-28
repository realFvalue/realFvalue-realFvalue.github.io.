# realFvalue-realFvalue.github.io
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CompTIA A+ Core 1 Exam Objectives Quiz</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            line-height: 1.6;
        }
        #quiz-container {
            background-color: #f0f0f0;
            padding: 20px;
            border-radius: 5px;
            margin-bottom: 20px;
        }
        #options-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
        }
        button {
            padding: 10px;
            font-size: 16px;
            cursor: pointer;
        }
        #feedback {
            margin-top: 20px;
            font-weight: bold;
        }
        #next-btn {
            display: none;
            margin-top: 20px;
        }
        #score, #progress {
            font-weight: bold;
            margin-top: 20px;
        }
        #category-select {
            margin-bottom: 20px;
        }
        @media screen and (max-width: 600px) {
            #options-container {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <h1>CompTIA A+ Core 1 Exam Objectives Quiz</h1>
    <select id="category-select">
        <option value="all">All Categories</option>
        <!-- Categories will be populated dynamically -->
    </select>
    <div id="quiz-container">
        <h2 id="question"></h2>
        <div id="options-container"></div>
    </div>
    <div id="feedback"></div>
    <div id="progress"></div>
    <button id="next-btn">Next Question</button>
    <div id="score"></div>

    <script>
    const quizData = {
        "Mobile Devices": [
            {
                question: "Which of the following is not a common mobile device form factor?",
                options: ["Smartphone", "Tablet", "Laptop", "Microwave"],
                correct: 3,
                explanation: "Microwave is not a mobile device form factor. Smartphones, tablets, and laptops are common mobile devices."
            },
            // Add more questions for this category
        ],
        "Networking": [
            {
                question: "What is the purpose of DHCP in a network?",
                options: ["To assign IP addresses automatically", "To secure network traffic", "To connect to the internet", "To manage network cables"],
                correct: 0,
                explanation: "DHCP (Dynamic Host Configuration Protocol) automatically assigns IP addresses to devices on a network."
            },
            // Add more questions for this category...
        ],
        "Hardware": [
            {
                question: "Which component is responsible for processing data in a computer?",
                options: ["RAM", "Hard Drive", "CPU", "Power Supply"],
                correct: 2,
                explanation: "The CPU (Central Processing Unit) is responsible for processing data in a computer."
            },
            // Add more questions for this category...
        ],
        "Virtualization and Cloud Computing": [
            {
                question: "What is the main benefit of virtualization?",
                options: ["Increased hardware costs", "Reduced energy consumption", "Slower performance", "Less efficient resource utilization"],
                correct: 1,
                explanation: "Virtualization typically leads to reduced energy consumption by allowing multiple virtual machines to run on a single physical server."
            },
            // Add more questions for this category...
        ],
        "Troubleshooting": [
            {
                question: "What is the first step in the troubleshooting process?",
                options: ["Implement the solution", "Establish a theory of probable cause", "Test the theory", "Identify the problem"],
                correct: 3,
                explanation: "The first step in the troubleshooting process is to identify the problem."
            },
            // Add more questions for this category...
        ]
    };

    let currentCategory = "all";
    let currentQuestions = [];
    let currentQuestionIndex = 0;
    let score = 0;

    const categorySelect = document.getElementById('category-select');
    const quizContainer = document.getElementById('quiz-container');
    const questionElement = document.getElementById('question');
    const optionsContainer = document.getElementById('options-container');
    const feedbackContainer = document.getElementById('feedback');
    const nextButton = document.getElementById('next-btn');
    const scoreContainer = document.getElementById('score');
    const progressContainer = document.getElementById('progress');

    function initializeQuiz() {
        // Populate category select
        for (let category in quizData) {
            let option = document.createElement('option');
            option.value = category;
            option.textContent = category;
            categorySelect.appendChild(option);
        }

        categorySelect.addEventListener('change', (e) => {
            currentCategory = e.target.value;
            startQuiz();
        });

        startQuiz();
    }

    function startQuiz() {
        currentQuestions = [];
        if (currentCategory === "all") {
            for (let category in quizData) {
                currentQuestions = currentQuestions.concat(quizData[category]);
            }
        } else {
            currentQuestions = quizData[currentCategory];
        }
        shuffleArray(currentQuestions);
        currentQuestionIndex = 0;
        score = 0;
        loadQuestion();
    }

    function shuffleArray(array) {
        for (let i = array.length - 1; i > 0; i--) {
            const j = Math.floor(Math.random() * (i + 1));
            [array[i], array[j]] = [array[j], array[i]];
        }
    }

    function loadQuestion() {
        if (currentQuestionIndex < currentQuestions.length) {
            const question = currentQuestions[currentQuestionIndex];
            questionElement.textContent = question.question;
            optionsContainer.innerHTML = '';
            question.options.forEach((option, index) => {
                const button = document.createElement('button');
                button.textContent = option;
                button.addEventListener('click', () => checkAnswer(index));
                optionsContainer.appendChild(button);
            });
            feedbackContainer.innerHTML = '';
            nextButton.style.display = 'none';
            updateProgress();
        } else {
            showFinalScore();
        }
    }

    function checkAnswer(selectedIndex) {
        const question = currentQuestions[currentQuestionIndex];
        const buttons = optionsContainer.getElementsByTagName('button');

        for (let button of buttons) {
            button.disabled = true;
        }

        if (selectedIndex === question.correct) {
            feedbackContainer.innerHTML = '<p style="color: green;">Correct!</p>';
            score++;
        } else {
            feedbackContainer.innerHTML = `<p style="color: red;">Incorrect. ${question.explanation}</p>`;
        }

        nextButton.style.display = 'block';
    }

    nextButton.addEventListener('click', () => {
        currentQuestionIndex++;
        loadQuestion();
    });

    function showFinalScore() {
        quizContainer.innerHTML = '<h2>Quiz Completed!</h2>';
        feedbackContainer.innerHTML = '';
        nextButton.style.display = 'none';
        scoreContainer.innerHTML = `Your final score: ${score} out of ${currentQuestions.length}`;
        progressContainer.innerHTML = '';
    }

    function updateProgress() {
        progressContainer.innerHTML = `Question ${currentQuestionIndex + 1} of ${currentQuestions.length}`;
    }

    initializeQuiz();
    </script>
</body>
</html>
