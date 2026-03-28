
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Advanced Chatbox</title>

<style>
body {
    font-family: Arial;
    background: #e5ddd5;
}

.chat-container {
    width: 360px;
    margin: 40px auto;
    background: #fff;
    border-radius: 10px;
    display: flex;
    flex-direction: column;
    height: 500px;
    box-shadow: 0 0 10px gray;
}

.header {
    background: #075e54;
    color: white;
    padding: 15px;
    text-align: center;
}

.chat-box {
    flex: 1;
    padding: 10px;
    overflow-y: auto;
}

.message {
    max-width: 70%;
    padding: 8px;
    margin: 8px 0;
    border-radius: 8px;
    font-size: 14px;
}

.user {
    background: #dcf8c6;
    align-self: flex-end;
}

.bot {
    background: #f1f0f0;
    align-self: flex-start;
}

.time {
    font-size: 10px;
    color: gray;
    display: block;
    margin-top: 3px;
}

.input-area {
    display: flex;
    border-top: 1px solid #ccc;
}

.input-area input {
    flex: 1;
    padding: 10px;
    border: none;
    outline: none;
}

.input-area button {
    background: #075e54;
    color: white;
    border: none;
    padding: 10px 15px;
    cursor: pointer;
}
</style>
</head>

<body>

<div class="chat-container">
    <div class="header">Chat App</div>

    <div class="chat-box" id="chatBox"></div>

    <div class="input-area">
        <input type="text" id="input" placeholder="Type message..." onkeypress="handleKey(event)">
        <button onclick="send()">Send</button>
    </div>
</div>

<script>
function getTime() {
    let now = new Date();
    return now.getHours() + ":" + now.getMinutes();
}

function send() {
    let input = document.getElementById("input");
    let text = input.value.trim();

    if (text === "") return;

    addMessage(text, "user");

    setTimeout(() => {
        botReply(text);
    }, 600);

    input.value = "";
}

function addMessage(text, type) {
    let chatBox = document.getElementById("chatBox");

    let msg = document.createElement("div");
    msg.classList.add("message", type);

    msg.innerHTML = text + "<span class='time'>" + getTime() + "</span>";

    chatBox.appendChild(msg);
    chatBox.scrollTop = chatBox.scrollHeight;
}

function botReply(text) {
    let reply = "I didn't understand 🤖";

    if (text.toLowerCase().includes("hi")) {
        reply = "Hello 👋";
    } else if (text.toLowerCase().includes("how are you")) {
        reply = "I'm fine 😊";
    } else if (text.toLowerCase().includes("name")) {
        reply = "I am ChatBot";
    }

    addMessage(reply, "bot");
}

function handleKey(event) {
    if (event.key === "Enter") {
        send();
    }
}
</script>

</body>
</html>

