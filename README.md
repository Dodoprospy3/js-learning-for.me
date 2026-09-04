<!DOCTYPE html>
<html>
    <head>
        <title>Rock Paper Scissors</title>
        <style> 
            * {
                cursor: url("icons8-cursor-32.svg") 0 0, auto;
            }

            body {
                background-color: rgb(25, 25, 25);
                color: white;
                font-family: Arial;
            }

            .play-button {
                background-color: rgb(25, 25, 25);
                height: 100px;
                width: 100px;
                font-size: 50px;
                border-radius: 50%;
                border-style: solid;
                border-width: 4px;
                border-color: white;
                margin-right: 10px;
                user-select: none;
            }

            .play-button:hover {
                filter: brightness(70%);
            }

            .play-button:active {
                filter: brightness(50%);
            }

            .reset-score-button {
                background-color: white;
                border: none;
                padding: 12px 22px 12px 22px;
                user-select: none;
            }

            .reset-score-button:hover {
                filter: brightness(70%);
            }

            .reset-score-button:active {
                filter: brightness(50%);
            }
        </style>
    </head>

    <body>
        <h1>Rock Paper Scissors</h1>

        <button class="play-button" onclick="
            playGame('rock');

        ">🪨</button> 

        <button class="play-button" onclick="
            playGame('paper');
        ">📰</button>

        <button class="play-button" onclick="
            playGame('scissors');
        ">✂️</button>

        <p class="js-result"></p>

        <p class="js-moves"></p>

        <p class="js-score" onclick="
            updateScoreElement();
        "></p>

        <button class="reset-score-button" onclick="
            score.wins = 0;
            score.losses = 0;
            score.ties = 0;
            localStorage.removeItem('score');
            updateScoreElement();
            document.querySelector('.js-result').innerHTML = '';
            document.querySelector('.js-moves').innerHTML = '';

/*
            alert(`Your Score Was Reset. 
Current Status: Wins: ${score.wins}, Losses: ${score.losses}, Ties: ${score.ties}.
            `);
*/
            ">Reset Score</button>

        <!--<button onclick="
            alert(scoreForAlert);
            ">check score</button>-->
        <!--<button onclick="
            console.log(localStorage.getItem('message'));
            ">check local storage</button>-->

        <script>
            let score = JSON.parse(localStorage.getItem('score')) || {
                    wins: 0,
                    losses: 0,
                    ties: 0
                }

            updateScoreElement();


/* uneeded if statement, leave for backup
            if (!score) {
                score = {
                    wins: 0,
                    losses: 0,
                    ties: 0
                };
            }
*/

            function playGame(playerMove) {
                const computerMove = pickComputerMove();

                let result = '';

                if (playerMove === 'scissors') {
                    if (computerMove === 'rock') {
                        result = 'You Lose.';
                    } else if (computerMove === 'paper') {
                        result = 'You Win!';
                    } else if (computerMove === 'scissors') {
                        result = 'Tie.';
                    }

                } else if (playerMove === 'paper') {
                    if (computerMove === 'rock') {
                        result = 'You Win!';
                    } else if (computerMove === 'paper') {
                        result = 'Tie.';
                    } else if (computerMove === 'scissors') {
                        result = 'You Lose.';
                    }

                } else if (playerMove === 'rock') {
                    if (computerMove === 'rock') {
                        result = 'Tie.';
                    } else if (computerMove === 'paper') {
                        result = 'You Lose.';
                    } else if (computerMove === 'scissors') {
                        result = 'You Win!';
                    }
                }

                if (result === 'You Win!') {
                    score.wins += 1;
                } else if (result === 'You Lose.') {
                    score.losses += 1;
                } else if (result === 'Tie.') {
                    score.ties += 1;
                }

                localStorage.setItem('score', JSON.stringify(score));

                document.querySelector('.js-result')
                    .innerHTML = result;

                document.querySelector('.js-moves')
                    .innerHTML = `You ${playerMove} - Computer ${computerMove}`;

                updateScoreElement();

            }


            function updateScoreElement() {
                document.querySelector('.js-score')
                    .innerHTML = `wins: ${score.wins}, losses: ${score.losses}, ties: ${score.ties}`
            }

            function pickComputerMove() {
                const randomNumber = Math.random();

                if (randomNumber >= 0 && randomNumber < 1 / 3) {
                    return 'rock';
                } else if (randomNumber >= 1 / 3 && randomNumber < 2 / 3) {
                    return 'paper';
                } else {
                    return 'scissors';
                }
            }
        </script>
    </body>
</html>
