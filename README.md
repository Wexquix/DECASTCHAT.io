<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DECAST CHAT</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background-image: url('https://r.resimlink.com/tywnFh.jpg');
            background-size: cover;
            background-position: center;
            transition: background-color 1s ease;
        }
        #chat-container {
            width: 400px;
            height: 600px;
            border-radius: 10px;
            box-shadow: 0 0 15px rgba(0, 0, 0, 0.2);
            overflow: hidden;
            display: flex;
            flex-direction: column;
            background-color: rgba(255, 255, 255, 0.9);
        }
        #header {
            background-color: #007bff;
            color: white;
            padding: 15px;
            text-align: center;
            font-size: 1.5em;
            font-weight: bold;
            border-bottom: 1px solid rgba(0, 0, 0, 0.1);
        }
        #chat-box {
            flex: 1;
            padding: 10px;
            overflow-y: auto;
            background-color: #f9f9f9;
        }
        .message {
            margin: 10px 0;
            padding: 10px;
            border-radius: 10px;
            background-color: rgba(224, 224, 224, 0.9);
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
            width: fit-content;
            max-width: 80%;
            transition: transform 0.3s;
        }
        .message:hover {
            transform: scale(1.05);
        }
        #message-input {
            display: flex;
            border-top: 1px solid #ccc;
            background-color: #fff;
            padding: 10px;
            box-shadow: 0 -2px 10px rgba(0, 0, 0, 0.1);
        }
        #message-input input {
            flex: 1;
            border: none;
            padding: 15px;
            font-size: 1em;
            border-radius: 10px 0 0 10px;
            box-shadow: inset 0 1px 3px rgba(0, 0, 0, 0.1);
        }
        #message-input button {
            border: none;
            background-color: #007bff;
            color: white;
            padding: 15px;
            font-size: 1em;
            cursor: pointer;
            border-radius: 0 10px 10px 0;
            transition: background-color 0.3s, transform 0.3s;
        }
        #message-input button:hover {
            background-color: #0056b3;
            transform: scale(1.05);
        }
    </style>
</head>
<body>
    <div id="chat-container">
        <div id="header">DECAST CHAT</div>
        <div id="chat-box"></div>
        <div id="message-input">
            <input type="text" id="message" placeholder="Mesajınızı yazın..." />
            <button onclick="sendMessage()">Gönder</button>
        </div>
    </div>

    <script>
        const chatBox = document.getElementById('chat-box');
        const messageInput = document.getElementById('message');
        const ws = new WebSocket('https://WexQuix.github.com/DECASTCHAT.i');

        ws.onmessage = (event) => {
            const messageElement = document.createElement('div');
            messageElement.classList.add('message');
            messageElement.textContent = event.data;
            chatBox.appendChild(messageElement);
            chatBox.scrollTop = chatBox.scrollHeight;
        };

        function sendMessage() {
            const message = messageInput.value;
            if (message.trim() === '') return;

            ws.send(message);
            messageInput.value = '';
        }

        // Arka plan rengini her dakika değiştir
        const colors = ['#FF5733', '#33FF57', '#3357FF', '#FF33A1', '#33FFF5'];
        let colorIndex = 0;

        function changeBackgroundColor() {
            document.body.style.backgroundColor = colors[colorIndex];
            colorIndex = (colorIndex + 1) % colors.length;
        }

        setInterval(changeBackgroundColor, 60000); // Her dakika renk değişimi
    </script>
</body>
</html>
