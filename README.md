<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>EDITOR WISHU CALL</title>

    <style>
        * {
            box-sizing: border-box;
        }

        body {
            margin: 0;
            font-family: Arial, sans-serif;
            background: linear-gradient(135deg, #06142e, #0755c9);
            color: white;
            text-align: center;
            min-height: 100vh;
            padding: 20px;
        }

        header {
            padding: 25px 10px;
        }

        .logo {
            width: 85px;
            height: 85px;
            background: #168cff;
            border-radius: 50%;
            display: grid;
            place-items: center;
            margin: auto;
            font-size: 42px;
            box-shadow: 0 0 25px #168cff;
        }

        h1 {
            color: #52c5ff;
            margin-bottom: 8px;
        }

        .container {
            max-width: 450px;
            margin: auto;
            padding: 25px;
            background: #10264a;
            border: 1px solid #2674d9;
            border-radius: 20px;
        }

        input {
            display: block;
            width: 100%;
            padding: 13px;
            margin: 12px 0;
            border-radius: 10px;
            border: 1px solid #4389db;
            background: #07152e;
            color: white;
        }

        button {
            width: 100%;
            padding: 13px;
            margin-top: 10px;
            border: none;
            border-radius: 10px;
            background: #168cff;
            color: white;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
        }

        button:hover {
            background: #0063d9;
        }

        video {
            width: 100%;
            margin-top: 15px;
            background: black;
            border-radius: 12px;
        }

        .warning {
            margin-top: 20px;
            padding: 15px;
            background: #382044;
            border-radius: 12px;
            font-size: 13px;
            line-height: 1.6;
        }

        .small {
            font-size: 12px;
            color: #b7d7ff;
            line-height: 1.5;
        }
    </style>
</head>

<body>

<header>
    <div class="logo">📞</div>
    <h1>EDITOR WISHU CALL</h1>
    <p>Connect With Your Friends</p>
</header>

<div class="container">

    <h2>🔐 Login / Register</h2>

    <p class="small">
        Google Sign-In must be connected for real accounts.
        Never enter your real Gmail password here.
    </p>

    <button onclick="googleLogin()">
        Continue With Google
    </button>

    <hr style="margin:25px 0; border-color:#2674d9;">

    <h2>📹 Video Call</h2>

    <input
        type="text"
        id="roomCode"
        placeholder="Enter Room Code"
    >

    <button onclick="startCamera()">
        Turn Camera On
    </button>

    <video
        id="myVideo"
        autoplay
        playsinline
        muted
    ></video>

    <button onclick="stopCamera()">
        Turn Camera Off
    </button>

    <p id="status" class="small">
        Camera is off.
    </p>

</div>

<div class="warning">
    <h3>🔞 Safety Rules</h3>

    <p>
        Adults only (18+). Nudity and sexual content are prohibited.
        Respect other users. Report inappropriate behaviour.
    </p>

    <p>
        This demo does not verify age or connect calls
        between different users.
    </p>
</div>

<script>

    let cameraStream = null;

    function googleLogin() {
        alert(
            "Google Sign-In is not connected yet. " +
            "Configure Google Authentication before using this feature."
        );
    }

    async function startCamera() {

        try {

            cameraStream =
                await navigator.mediaDevices.getUserMedia({
                    video: true,
                    audio: true
                });

            document.getElementById("myVideo").srcObject =
                cameraStream;

            document.getElementById("status").textContent =
                "Camera and microphone are on.";

        } catch (error) {

            document.getElementById("status").textContent =
                "Camera unavailable. Allow camera permissions.";

        }
    }

    function stopCamera() {

        if (cameraStream) {

            cameraStream.getTracks().forEach(track => {
                track.stop();
            });

            cameraStream = null;
        }

        document.getElementById("myVideo").srcObject = null;

        document.getElementById("status").textContent =
            "Camera is off.";
    }

</script>

</body>
</html>
