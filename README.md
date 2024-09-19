# stopWatch
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="stopWatch.css">
    <title>Stopwatch</title>
</head>
<body>
    <div class="stopwatch">
        <div class="timerDisplay">00:00:00</div>
    </div>

   <div class="button">
    <div class="btn" id="startBtn" style="--clr:green">Start</div>
    <div class="btn" id="resetBtn" style="--clr:blue">Reset</div>
    <div class="btn" id="stopBtn" style="--clr:red">Stop</div>
   </div>

    <script src="stopWatch.js"></script>
</body>
</html>

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: Verdana, Geneva, Tahoma, sans-serif;
}

body {
    background-color: rgba(0,0,0,0.7);
    color: #ffffff;
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    flex-direction:column;
    
}

.stopwatch {
    background-color: rgba(0,0,0,0.9);
    border-radius: 10px;
    padding: 20px 24px;
}

.timerDisplay {
    font-size: 50px;
    font-weight: 600;
}

.button {
    margin: 20px;
    display:flex;
}

.btn {
    background: none;
    border: none;
    color: #fff;
    background-color: var(--clr);
    padding: 10px 20px;
    margin-inline: 12px;
    cursor: pointer;
    border-radius: 8px;
    display:flex;
}


let timerDisplay = document.querySelector('.timerDisplay');
let stopBtn = document.getElementById('stopBtn');
let startBtn = document.getElementById('startBtn');
let resetBtn = document.getElementById('resetBtn');

let msec = 0;
let secs = 0;
let mins = 0;

let timerId = null;

startBtn.addEventListener('click', function () {
    if (timerId !== null) {
        clearInterval(timerId);
    }
    timerId = setInterval(startTimer, 10);
});

stopBtn.addEventListener('click', function () {
    clearInterval(timerId);
});

resetBtn.addEventListener('click', function () {
    clearInterval(timerId);
    timerDisplay.innerHTML = `00:00:00`;
    msec = secs = mins = 0;
});

function startTimer() {
    msec++;
    if (msec === 100) {
        msec = 0;
        secs++;
        if (secs === 60) {
            secs = 0;
            mins++;
        }
    }

    let msecString = msec < 10 ? `0${msec}` : msec;
    let secsString = secs < 10 ? `0${secs}` : secs;
    let minsString = mins < 10 ? `0${mins}` : mins;

    timerDisplay.innerHTML = `${minsString}:${secsString}:${msecString}`;
}
