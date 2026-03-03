<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Countdown Timer</title>
    <style>
        body {font-family: Arial, sans-serif;}
        .countdown {font-size: 32px; font-weight: bold;}
    </style>
</head>
<body>
    <h1>Countdown Timer</h1>
    <div class="countdown" id="countdown"></div>

    <script>
        // Set the date we're counting down to
        const countdownDate = new Date('2026-03-03T22:52:41Z').getTime();

        // Update the countdown every 1 second
        const x = setInterval(function() {
            const now = new Date().getTime();
            const distance = countdownDate - now;

            // Time calculations for days, hours, minutes and seconds
            const days = Math.floor(distance / (1000 * 60 * 60 * 24));
            const hours = Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
            const minutes = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60));
            const seconds = Math.floor((distance % (1000 * 60)) / 1000);

            // Display the result in the countdown div
            document.getElementById("countdown").innerHTML = days + "d " + hours + "h " + minutes + "m " + seconds + "s ";

            // If the countdown is over, display a message
            if (distance < 0) {
                clearInterval(x);
                document.getElementById("countdown").innerHTML = "EXPIRED";
            }
        }, 1000);
    </script>
</body>
</html>