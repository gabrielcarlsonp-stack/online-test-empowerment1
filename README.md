<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Equality Awareness Test</title>

<style>
* {
    box-sizing: border-box;
    font-family: "Times New Roman", Georgia, serif;
}

body {
    margin: 0;
    background: #ffffff;
    color: #000000;
    overflow-x: hidden;
}

/* Screens */
.screen {
    display: none;
    min-height: 100vh;
    justify-content: center;
    align-items: center;
    text-align: center;
    padding: 20px;
    animation: fadeIn 0.8s ease;
}
.active {
    display: flex;
    flex-direction: column;
}

/* Animations */
@keyframes fadeIn {
    from {opacity:0; transform: translateY(10px);}
    to {opacity:1; transform: translateY(0);}
}

.title {
    font-size: 2.3em;
    margin-bottom: 10px;
    letter-spacing: 2px;
}

.subtitle {
    opacity: 0.7;
    margin-bottom: 30px;
}

.card {
    background: #ffffff;
    padding: 30px;
    border-radius: 0px;
    max-width: 650px;
    width: 100%;
    border: 2px solid #000000;
}

/* Buttons */
button {
    padding: 12px 30px;
    border: 2px solid black;
    font-size: 16px;
    cursor: pointer;
    background: black;
    color: white;
    font-weight: bold;
    transition: 0.3s;
    margin-top: 20px;
}
button:hover {
    background: white;
    color: black;
}

/* Options */
.option {
    border: 1px solid black;
    padding: 12px;
    margin: 10px 0;
    cursor: pointer;
    transition: 0.2s;
}
.option:hover {
    background: black;
    color: white;
}

/* Progress */
.progress {
    margin-bottom: 10px;
    font-size: 14px;
    opacity: 0.8;
}
</style>
</head>
<body>

<!-- 🔊 AUDIO -->
<audio id="bgm" loop>
    <source src="bgm.mp3" type="audio/mpeg">
</audio>

<audio id="clickSound">
    <source src="click.mp3" type="audio/mpeg">
</audio>

<audio id="correctSound">
    <source src="correct.mp3" type="audio/mpeg">
</audio>

<audio id="wrongSound">
    <source src="wrong.mp3" type="audio/mpeg">
</audio>

<audio id="finishSound">
    <source src="finish.mp3" type="audio/mpeg">
</audio>

<!-- INTRO -->
<div id="intro" class="screen active">
    <div class="card">
        <div class="title">EQUALITY AWARENESS TEST</div>
        <div class="subtitle">
            Stop Strand Discrimination <br>
            We Are All Equal
        </div>
        <p>
            This formal assessment aims to promote respect, fairness, and equality among students.
        </p>
        <button onclick="startTest()">BEGIN</button>
    </div>
</div>

<!-- QUIZ -->
<div id="quiz" class="screen">
    <div class="card">
        <div class="progress" id="progress"></div>
        <h2 id="question"></h2>
        <div id="options"></div>
    </div>
</div>

<!-- RESULT -->
<div id="result" class="screen">
    <div class="card">
        <div class="title">ASSESSMENT COMPLETED</div>
        <h2 id="scoreText"></h2>
        <p>
            Always remember: Your strand does not define your value. <br>
            Every student deserves equal respect.
        </p>
        <button onclick="location.reload()">RESTART</button>
    </div>
</div>

<script>
const questions = [
    { q: "What does equality mean in school?", o: ["Everyone is treated fairly", "Only top students matter", "Some strands are better", "Only honors students are important"], a: 0 },
    { q: "Why should we stop strand discrimination?", o: ["It causes division", "It hurts others", "It is unfair", "All of the above"], a: 3 },
    { q: "Students from different strands are...", o: ["Not equal", "Less important", "All valuable", "Not needed"], a: 2 },
    { q: "Respect means...", o: ["Judging others", "Ignoring others", "Treating everyone with dignity", "Choosing favorites"], a: 2 },
    { q: "If someone is different, you should...", o: ["Make fun of them", "Avoid them", "Respect them", "Judge them"], a: 2 },
    { q: "Which behavior supports equality?", o: ["Bullying", "Helping others", "Discriminating", "Excluding others"], a: 1 },
    { q: "Strand discrimination can cause...", o: ["Friendship", "Motivation", "Conflict and sadness", "Success"], a: 2 },
    { q: "All students have the right to...", o: ["Be respected", "Be ignored", "Be judged", "Be excluded"], a: 0 },
    { q: "A good student should...", o: ["Look down on others", "Support classmates", "Only care about grades", "Avoid other strands"], a: 1 },
    { q: "Equality in school helps build...", o: ["Hate", "Fear", "A positive community", "Division"], a: 2 }
];

let index = 0;
let score = 0;

const bgm = document.getElementById("bgm");
const clickSound = document.getElementById("clickSound");
const correctSound = document.getElementById("correctSound");
const wrongSound = document.getElementById("wrongSound");
const finishSound = document.getElementById("finishSound");

function startTest() {
    clickSound.play();
    bgm.volume = 0.3;
    bgm.play();

    document.getElementById("intro").classList.remove("active");
    document.getElementById("quiz").classList.add("active");
    showQuestion();
}

function showQuestion() {
    const q = questions[index];
    document.getElementById("progress").innerText = `Question ${index + 1} of ${questions.length}`;
    document.getElementById("question").innerText = q.q;

    const optionsDiv = document.getElementById("options");
    optionsDiv.innerHTML = "";

    q.o.forEach((opt, i) => {
        const div = document.createElement("div");
        div.className = "option";
        div.innerText = opt;
        div.onclick = () => selectAnswer(i);
        optionsDiv.appendChild(div);
    });
}

function selectAnswer(choice) {
    if (choice === questions[index].a) {
        correctSound.play();
        score++;
    } else {
        wrongSound.play();
    }

    index++;
    if (index < questions.length) {
        setTimeout(showQuestion, 400);
    } else {
        showResult();
    }
}

function showResult() {
    bgm.pause();
    finishSound.play();

    document.getElementById("quiz").classList.remove("active");
    document.getElementById("result").classList.add("active");

    document.getElementById("scoreText").innerText =
        `Final Score: ${score} / ${questions.length}`;
}
</script>

</body>
</html>

