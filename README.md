
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Real-Time Chat</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background-color: #f4f4f4;
        }

        .chat-container {
            width: 500px;
            max-width: 90%;
            background-color: white;
            padding: 20px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            border-radius: 10px;
        }

        h1 {
            text-align: center;
        }

        #onlineUsers {
            text-align: center;
            font-weight: bold;
            color: green;
            margin-bottom: 20px;
        }

        #messages {
            border: 1px solid #ccc;
            padding: 10px;
            margin-bottom: 20px;
            height: 200px;
            overflow-y: auto;
        }

        #messageInput {
            width: calc(100% - 22px);
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }

        button {
            width: 100%;
            padding: 10px;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            margin-top: 10px;
        }

        button:hover {
            background-color: #45a049;
        }
    </style>
</head>
<body>

<div class="chat-container">
    <h1>Real-Time Chat</h1>
    <div id="onlineUsers">Online Users: 0</div>
    <div id="messages"></div>
    <input type="text" id="messageInput" placeholder="Enter your message...">
    <button onclick="sendMessage()">Send Message</button>
</div>

<script>
    const ws = new WebSocket('ws://localhost:8080');

    ws.onmessage = (event) => {
        const data = JSON.parse(event.data);

        if (data.type === 'online') {
            document.getElementById('onlineUsers').textContent = `Online Users: ${data.count}`;
        } else if (data.type === 'message') {
            const messagesDiv = document.getElementById('messages');
            messagesDiv.innerHTML += `<div>${data.text}</div>`;
            messagesDiv.scrollTop = messagesDiv.scrollHeight;
        }
    };

    function sendMessage() {
        const messageInput = document.getElementById('messageInput');
        const message = messageInput.value;

        if (message) {
            ws.send(JSON.stringify({ type: 'message', text: message }));
            messageInput.value = '';
        }
    }
</script>

</body>
</html>
