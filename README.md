
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Password Generator</title>
<link rel="stylesheet" href="styles.css">
</head>
<body>
  <style>
    /* Import Bootstrap CSS (Assuming you have Bootstrap linked in your project) */
@import url('https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/css/bootstrap.min.css');

/* Custom CSS */

body {
  background-color: #000204;
  font-family: 'Arial', sans-serif;
}

.container {
  background-color: #fff;
  padding: 30px;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  text-align: center;
  max-width: 600px;
  margin-top: 50px;
}

h1 {
  font-size: 28px;
  margin-bottom: 30px;
  display:none;
}

.form-group {
  margin-bottom: 20px;
  text-align: left;
}

.label-checkbox {
  margin-right: 15px;
}

.password-container {
  margin-top: 30px;
}

#password {
  font-family: 'Courier New', monospace;
  font-size: 18px;
  background-color: #f9f9f9;
  padding: 15px;
  border: 1px solid #ccc;
  border-radius: 4px;
  display: inline-block;
  word-break: break-all;
  min-width: 250px;
}

button {
  font-size: 16px;
  margin-top: 15px;
}
#exitLogo {
  position: absolute;
  top: 10px;
  right: 10px;
  width: 50px; /* Fixed width */
  height: 50px; /* Fixed height */
  display: flex;
  justify-content: center;
  align-items: center;
}

#exitLogo img {
  width: 100%;
  height: 100%;
  object-fit: contain; /* Maintain aspect ratio */
}
  </style>
<div class="container">
  
  <h1>Password Generator</h1>
  <div class="form-group">
    <label for="length">Password Length:</label>
    <input type="number" id="length" min="4" max="32" value="12">
  </div>
  <div class="form-group">
    <label for="characters">Include:</label>
    <input type="checkbox" id="uppercase" checked><br>
    <label for="uppercase">Uppercase Letters</label>
    <input type="checkbox" id="lowercase" checked><br>
    <label for="lowercase">Lowercase Letters</label>
    <input type="checkbox" id="numbers" checked><br>
    <label for="numbers">Numbers</label>
    <input type="checkbox" id="symbols" checked><br>
    <label for="symbols">Symbols (!@#$%^&*()_+)</label>
  </div>
  <div class="form-group">
    <button id="generate">Generate Password</button>
    <button id="copy" disabled>Copy to Clipboard</button>
  </div>
  <div class="password-container">
    <p id="password"></p>
    
  </div>
</div>
<a href="https://igtradingmaster.github.io/Home/" id="exitLogo">
  <img src="https://t3.ftcdn.net/jpg/04/51/52/52/360_F_451525222_IKqxMEeAVBS6Pj5JpJU0MxnQAtasHZPe.jpg" alt="Exit Logo">
</a>

<script>
  const lengthField = document.getElementById('length');
const uppercaseCheckbox = document.getElementById('uppercase');
const lowercaseCheckbox = document.getElementById('lowercase');
const numbersCheckbox = document.getElementById('numbers');
const symbolsCheckbox = document.getElementById('symbols');
const generateButton = document.getElementById('generate');
const copyButton = document.getElementById('copy');
const passwordField = document.getElementById('password');

generateButton.addEventListener('click', function() {
  const length = +lengthField.value;
  const includeUppercase = uppercaseCheckbox.checked;
  const includeLowercase = lowercaseCheckbox.checked;
  const includeNumbers = numbersCheckbox.checked;
  const includeSymbols = symbolsCheckbox.checked;

  const generatedPassword = generatePassword(length, includeUppercase, includeLowercase, includeNumbers, includeSymbols);
  animateText(generatedPassword);
  passwordField.textContent = generatedPassword;
  copyButton.disabled = false;
});

copyButton.addEventListener('click', function() {
  const textarea = document.createElement('textarea');
  const password = passwordField.textContent;

  if (!password) {
    return;
  }

  textarea.value = password;
  document.body.appendChild(textarea);
  textarea.select();
  document.execCommand('copy');
  textarea.remove();
});

function generatePassword(length, uppercase, lowercase, numbers, symbols) {
  let charSet = '';
  if (uppercase) charSet += 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
  if (lowercase) charSet += 'abcdefghijklmnopqrstuvwxyz';
  if (numbers) charSet += '0123456789';
  if (symbols) charSet += '!@#$%^&*()_+';

  let password = '';
  for (let i = 0; i < length; i++) {
    const randomIndex = Math.floor(Math.random() * charSet.length);
    password += charSet[randomIndex];
  }

  return password;
}

function animateText(text) {
  let index = 0;
  const interval = setInterval(function() {
    passwordField.textContent = text.substring(0, index + 1);
    index++;

    if (index >= text.length) {
      clearInterval(interval);
    }
  }, 50); // Adjust the interval (in milliseconds) for typing speed
}

</script>
</body>
