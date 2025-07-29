document.addEventListener('DOMContentLoaded', () => {
    const circles = document.querySelectorAll('.circle');
    const targetColorText = document.getElementById('target-color-text');
    const scoreValue = document.getElementById('score-value');
    const startButton = document.getElementById('start-button');
    const gameMessage = document.getElementById('game-message');

    let score = 0;
    let targetColor = '';
    let gameActive = false;

    // Define colors and their names
    const colors = {
        red: '#FF0000',
        blue: '#0000FF',
        green: '#008000',
        yellow: '#FFFF00',
        purple: '#800080',
        orange: '#FFA500'
    };
    const colorNames = Object.keys(colors);

    // Load sounds
    const correctSound = new Audio('sounds/correct.wav');
    const wrongSound = new Audio('sounds/wrong.wav');

    // Function to play sound
    function playSound(sound) {
        sound.currentTime = 0; // Rewind to start if already playing
        sound.play().catch(e => console.error("Error playing sound:", e));
    }

    // Function to set up a new round
    function newRound() {
        if (!gameActive) return;

        // Reset message
        gameMessage.textContent = '';

        // Randomly assign colors to circles
        const shuffledColors = [...colorNames].sort(() => 0.5 - Math.random());
        circles.forEach((circle, index) => {
            const colorName = shuffledColors[index];
            circle.style.backgroundColor = colors[colorName];
            circle.dataset.color = colorName; // Store color name in data attribute
        });

        // Choose a random target color
        targetColor = colorNames[Math.floor(Math.random() * colorNames.length)];
        targetColorText.textContent = targetColor.toUpperCase();
    }

    // Handle circle click
    circles.forEach(circle => {
        circle.addEventListener('click', () => {
            if (!gameActive) return;

            const clickedColor = circle.dataset.color;
            if (clickedColor === targetColor) {
                score++;
                scoreValue.textContent = score;
                playSound(correctSound);
                gameMessage.textContent = 'Benar!';
                gameMessage.style.color = '#aaffaa';
            } else {
                score = Math.max(0, score - 1); // Decrease score, but not below 0
                scoreValue.textContent = score;
                playSound(wrongSound);
                gameMessage.textContent = `Salah! Itu ${clickedColor}.`;
                gameMessage.style.color = '#ff6666';
            }
            // Start a new round after a short delay
            setTimeout(newRound, 700);
        });
    });

    // Start game function
    startButton.addEventListener('click', () => {
        score = 0;
        scoreValue.textContent = score;
        gameActive = true;
        startButton.classList.add('hidden'); // Hide start button
        gameMessage.textContent = 'Mulai!';
        gameMessage.style.color = '#ffdd57';
        // Show circles if they were hidden (e.g., after game over)
        circles.forEach(circle => circle.classList.remove('hidden'));
        targetColorText.parentElement.classList.remove('hidden'); // Show instruction
        scoreValue.parentElement.classList.remove('hidden'); // Show score
        setTimeout(newRound, 1000); // Start first round after a short delay
    });

    // Initial setup: hide game elements until start button is clicked
    circles.forEach(circle => circle.classList.add('hidden'));
    targetColorText.parentElement.classList.add('hidden'); // Hide instruction
    scoreValue.parentElement.classList.add('hidden'); // Hide score
    gameMessage.textContent = 'Tekan "Mulai Game" untuk bermain!';
});
