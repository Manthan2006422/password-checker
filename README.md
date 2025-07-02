
<!DOCTYPE html><html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Password Strength Checker</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f4f4f4;
      padding: 20px;
    }
    .container {
      background: white;
      max-width: 500px;
      margin: auto;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
    }
    .strength-bar {
      height: 10px;
      background: lightgray;
      border-radius: 5px;
      margin-top: 5px;
    }
    .feedback {
      margin-top: 10px;
      font-size: 14px;
    }
    .strong { background: green; width: 100%; }
    .medium { background: orange; width: 66%; }
    .weak { background: red; width: 33%; }
  </style>
</head>
<body>
  <div class="container">
    <h2>Password Strength Checker</h2>
    <input type="password" id="password" placeholder="Enter your password" style="width:100%; padding: 10px;">
    <div class="strength-bar" id="strength-bar"></div>
    <div class="feedback" id="feedback"></div>
  </div>  <script>
    const passwordInput = document.getElementById('password');
    const strengthBar = document.getElementById('strength-bar');
    const feedback = document.getElementById('feedback');

    passwordInput.addEventListener('input', () => {
      const pwd = passwordInput.value;
      let score = 0;
      let tips = [];

      // Criteria checks
      if (pwd.length >= 12) score++; else tips.push("Make it at least 12 characters long.");
      if (/[a-z]/.test(pwd)) score++; else tips.push("Add lowercase letters.");
      if (/[A-Z]/.test(pwd)) score++; else tips.push("Add uppercase letters.");
      if (/[0-9]/.test(pwd)) score++; else tips.push("Add numbers.");
      if (/[^a-zA-Z0-9]/.test(pwd)) score++; else tips.push("Add special characters (e.g., !, @, #).");

      // Common pattern checks
      const commonPatterns = ["123456", "password", "qwerty", "letmein"];
      if (commonPatterns.some(pattern => pwd.toLowerCase().includes(pattern))) {
        tips.push("Avoid common patterns like '123456', 'password', etc.");
        score = Math.max(score - 1, 0);
      }

      // Display strength bar
      if (score >= 4) {
        strengthBar.className = 'strength-bar strong';
        feedback.innerHTML = "✅ Strong password";
      } else if (score >= 2) {
        strengthBar.className = 'strength-bar medium';
        feedback.innerHTML = "⚠️ Medium password<br>" + tips.join('<br>');
      } else {
        strengthBar.className = 'strength-bar weak';
        feedback.innerHTML = "❌ Weak password<br>" + tips.join('<br>');
      }
    });
  </script></body>
</html>

