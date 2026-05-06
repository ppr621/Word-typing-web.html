<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Speed Typing Test</title>
    <style>
        body { font-family: sans-serif; display: flex; flex-direction: column; align-items: center; padding: 20px; background: #f4f4f9; }
        .container { background: white; padding: 2rem; border-radius: 8px; box-shadow: 0 2px 10px rgba(0,0,0,0.1); width: 100%; max-width: 600px; }
        #text-display { font-size: 1.2rem; margin-bottom: 1rem; color: #333; line-height: 1.5; }
        #input-area { width: 100%; padding: 10px; font-size: 1rem; box-sizing: border-box; }
        .result { margin-top: 20px; font-weight: bold; }
        button { margin-top: 10px; padding: 10px 20px; cursor: pointer; }
    </style>
</head>
<body>

<div class="container">
    <h2>Typing Speed Test</h2>
    <p id="text-display">The quick brown fox jumps over the lazy dog.</p>
    <input type="text" id="input-area" placeholder="Start typing here..." disabled>
    <div id="result" class="result"></div>
    <button onclick="startTest()">Start / Restart</button>
</div>

<script>
    const display = document.getElementById('text-display');
    const input = document.getElementById('input-area');
    const result = document.getElementById('result');
    let startTime;

    function startTest() {
        input.value = '';
        input.disabled = false;
        input.focus();
        result.textContent = '';
        startTime = new Date().getTime();
    }

    input.addEventListener('input', () => {
        const text = display.textContent;
        const typed = input.value;

        // Check if finished
        if (typed.length === text.length) {
            const endTime = new Date().getTime();
            const timeTaken = (endTime - startTime) / 1000;
            
            // Character-by-character validation
            if (typed === text) {
                const words = text.split(' ').length;
                const wpm = Math.round((words / (timeTaken / 60)));
                result.innerHTML = `<span style="color: green;">Correct!</span> Speed: ${wpm} WPM`;
            } else {
                result.innerHTML = `<span style="color: red;">Incorrect.</span> Please try again.`;
            }
            input.disabled = true;
        }
    });
</script>
</body>
</html>
b