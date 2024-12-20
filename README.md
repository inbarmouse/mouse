<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>YouTube Music Player with API</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin-top: 50px;
        }
        #timer {
            font-size: 24px;
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <h1>YouTube Music Player</h1>

    <!-- Embedded YouTube video container -->
    <div id="player"></div>

    <div id="timer">Time Remaining: 20:00</div>

    <script>
        let timer;
        let duration = 20 * 60; // 20 minutes in seconds

        // This function is called when the API is ready
        function onYouTubeIframeAPIReady() {
            player = new YT.Player('player', {
                height: '315',
                width: '560',
                videoId: 'NM529E00pAM',
                playerVars: {
                    'autoplay': 1, // autoplay video
                    'controls': 0, // hide controls to prevent pausing
                    'rel': 0, // disable related videos at the end
                    'showinfo': 0 // disable video info display
                },
                events: {
                    'onReady': onPlayerReady,
                }
            });
        }

        function onPlayerReady(event) {
            // Start the timer when the video is ready
            startMusic();
        }

        function startMusic() {
            // Start the timer
            updateTimer();
            timer = setInterval(updateTimer, 1000);

            // Stop video after 20 minutes
            setTimeout(() => {
                clearInterval(timer);
                player.stopVideo(); // stop the video
                document.getElementById('timer').innerText = "Music finished";
            }, duration * 1000);
        }

        function updateTimer() {
            const minutes = Math.floor(duration / 60);
            const seconds = duration % 60;
            document.getElementById('timer').innerText = `Time Remaining: ${minutes}:${seconds < 10 ? '0' : ''}${seconds}`;
            duration--;
        }

        // Load the YouTube Iframe API script
        const script = document.createElement('script');
        script.src = "https://www.youtube.com/iframe_api";
        document.body.appendChild(script);
    </script>
</body>
</html>
