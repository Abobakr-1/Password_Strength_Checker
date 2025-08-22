<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Password Strength Checker</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
      background: #0d1117;
      color: #e6edf3;
    }

    .box {
      background: #161b22;
      padding: 50px; /* زودنا المسافة الداخلية */
      border-radius: 15px;
      box-shadow: 0px 0px 20px rgba(0,0,0,0.6);
      text-align: center;
      width: 450px;   /* العرض أكبر */
    }

    h1 {
      margin-bottom: 25px;
      color: #58a6ff;
      font-size: 26px; /* خط أكبر */
    }

    input[type="password"],
    input[type="text"] {
      padding: 12px;
      width: 100%;
      border: 2px solid #30363d;
      border-radius: 8px;
      background: #0d1117;
      color: white;
      outline: none;
      margin-bottom: 12px;
      font-size: 16px;
    }

    label {
      font-size: 15px;
      cursor: pointer;
      display: block;
      text-align: left;
    }

    #strength {
      margin-top: 20px;
      font-weight: bold;
      font-size: 20px;
    }

    /* Progress bar */
    .progress {
      width: 100%;
      height: 15px;  /* أعلى من قبل */
      border-radius: 8px;
      background: #30363d;
      margin-top: 15px;
      overflow: hidden;
    }

    .progress-bar {
      height: 100%;
      width: 0%;
      transition: width 0.4s ease-in-out;
    }

    .weak { background: #f85149; }
    .medium { background: #d29922; }
    .strong { background: #3fb950; }
  </style>
</head>
<body>
  <div class="box">
    <h1>Password Strength Checker 🔐</h1>
    
    <input type="password" id="password" placeholder="Enter your password..." oninput="checkStrength()">
    <label>
      <input type="checkbox" onclick="togglePassword()"> Show Password
    </label>

    <div class="progress">
      <div class="progress-bar" id="progress-bar"></div>
    </div>

    <div id="strength"></div>
  </div>

  <script>
    function togglePassword() {
      const passField = document.getElementById("password");
      passField.type = passField.type === "password" ? "text" : "password";
    }

    function checkStrength() {
      const password = document.getElementById("password").value;
      const strengthDiv = document.getElementById("strength");
      const progressBar = document.getElementById("progress-bar");

      let strength = 0;

      if (password.length >= 8) strength++;
      if (/[A-Z]/.test(password)) strength++;
      if (/[a-z]/.test(password)) strength++;
      if (/[0-9]/.test(password)) strength++;
      if (/[^A-Za-z0-9]/.test(password)) strength++;

      if (password.length === 0) {
        strengthDiv.textContent = "";
        progressBar.style.width = "0%";
        progressBar.className = "progress-bar";
        return;
      }

      if (strength <= 2) {
        strengthDiv.textContent = "Weak ❌";
        strengthDiv.style.color = "#f85149";
        progressBar.style.width = "33%";
        progressBar.className = "progress-bar weak";
      } else if (strength === 3 || strength === 4) {
        strengthDiv.textContent = "Medium ⚠️";
        strengthDiv.style.color = "#d29922";
        progressBar.style.width = "66%";
        progressBar.className = "progress-bar medium";
      } else {
        strengthDiv.textContent = "Strong ✅";
        strengthDiv.style.color = "#3fb950";
        progressBar.style.width = "100%";
        progressBar.className = "progress-bar strong";
      }
    }
  </script>
</body>
</html>
