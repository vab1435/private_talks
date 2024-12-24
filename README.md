<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Encrypted Messenger</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f9;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }
        .container {
            background-color: white;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
            width: 400px;
        }
        h1 {
            text-align: center;
            font-size: 24px;
            color: #333;
        }
        textarea, input[type="number"], button {
            width: 100%;
            padding: 10px;
            margin-bottom: 15px;
            font-size: 16px;
            border-radius: 5px;
            border: 1px solid #ddd;
        }
        button {
            background-color: #4CAF50;
            color: white;
            border: none;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        button:hover {
            background-color: #45a049;
        }
        .result-box {
            background-color: #f0f0f0;
            padding: 10px;
            font-family: monospace;
            word-wrap: break-word;
            height: 120px;
        }
    </style>
</head>
<body>

<div class="container">
    <h1>Encrypted Messenger</h1>

    <label for="message">Enter your message:</label>
    <textarea id="message" placeholder="Enter text here..."></textarea>

    <label for="pin">Enter your PIN:</label>
    <input type="number" id="pin" placeholder="Enter PIN" />

    <button onclick="encryptMessage()">Encrypt</button>
    <button onclick="decryptMessage()">Decrypt</button>

    <h2>Result:</h2>
    <div class="result-box" id="result"></div>
</div>

<script>
    function encrypt(text, pin) {
        let encryptedText = '';
        for (let i = 0; i < text.length; i++) {
            let char = text[i];
            if (/[a-zA-Z]/.test(char)) {
                let shift = pin % 26; 
                if (char >= 'a' && char <= 'z') {
                    encryptedText += String.fromCharCode((char.charCodeAt(0) - 97 + shift) % 26 + 97);
                } else if (char >= 'A' && char <= 'Z') {
                    encryptedText += String.fromCharCode((char.charCodeAt(0) - 65 + shift) % 26 + 65);
                }
            } else {
                encryptedText += char; 
            }
        }
        return encryptedText;
    }

    function decrypt(text, pin) {
        let decryptedText = '';
        for (let i = 0; i < text.length; i++) {
            let char = text[i];
            if (/[a-zA-Z]/.test(char)) {
                let shift = pin % 26; 
                if (char >= 'a' && char <= 'z') {
                    decryptedText += String.fromCharCode((char.charCodeAt(0) - 97 - shift + 26) % 26 + 97);
                } else if (char >= 'A' && char <= 'Z') {
                    decryptedText += String.fromCharCode((char.charCodeAt(0) - 65 - shift + 26) % 26 + 65);
                }
            } else {
                decryptedText += char; 
            }
        }
        return decryptedText;
    }

    function encryptMessage() {
        const message = document.getElementById("message").value;
        const pin = parseInt(document.getElementById("pin").value);
        const encryptedText = encrypt(message, pin);
        document.getElementById("result").textContent = encryptedText;
    }

    function decryptMessage() {
        const message = document.getElementById("message").value;
        const pin = parseInt(document.getElementById("pin").value);
        const decryptedText = decrypt(message, pin);
        document.getElementById("result").textContent = decryptedText;
    }
</script>

</body>
</html>
