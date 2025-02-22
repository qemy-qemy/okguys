<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Secure Owner Portal</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    <style>
        :root {
            --primary-color: #2a5298;
            --secondary-color: #1e3c72;
            --error-color: #ff4444;
            --success-color: #00C851;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', sans-serif;
        }

        body {
           background-image: url("OPg") ;
            min-height: 100vh;
            background-repeat: no-repeat;
         background-size: 70% 600px;
         background: linear-gradient(45deg,rgb(2, 48, 116),rgb(1, 3, 12),rgb(121, 149, 242));
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
            box-shadow: inset 1000px 50000px 5000px rgba(0, 0, 0, 0.5);
        }

        .wrapper {
            display: flex;
            align-items: center;
            justify-content: center;
            width: 100%;
            max-width: 900px;
            gap: 20px;
        }

        .image-container {
            flex: 1;
            display: flex;
            justify-content: center;
        }

        .image-container img {
            height: 75vh;
            max-width: 100%;
        }

        .container {
            flex: 1;
            background: white;
            padding: 2rem;
            border-radius: 15px;
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
            max-width: 400px;
            transition: transform 0.3s ease;
            position: relative;
            overflow: hidden;
            border: 1px solid rgb(181, 150, 247);
           
        }

        h2 {
            color: var(--primary-color);
            text-align: center;
            margin-bottom: 1.5rem;
            font-size: 1.8rem;
            font-weight: 700;
        }

        .form-group {
            margin-bottom: 1.5rem;
            position: relative;
            color: white;
        }

        label {
            display: block;
            margin-bottom: 0.6rem;
            color: #444;
            font-weight: 600;
            font-size: 1rem;
        }

        input {
            width: 100%;
            padding: 12px;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            font-size: 1rem;
            transition: all 0.3s ease;
            padding-right: 40px;
        }

        input:focus {
            border-color: var(--primary-color);
            box-shadow: 0 0 0 3px rgba(42, 82, 152, 0.1);
            outline: none;
        }

        button {
            width: 200px;
            padding: 12px;
            background-color: rgb(255, 188, 5);
            color: white;
            margin-left: 4rem;
            border: none;
            border-radius: 8px;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 1s ease;
            position: relative;
        }

        button:hover {
            color: #c44c02;
            opacity: 200;
        }

        #message {
            margin-top: 1rem;
            padding: 12px;
            border-radius: 8px;
            font-weight: 500;
            text-align: center;
            opacity: 0;
            transform: translateY(-10px);
            transition: all 0.4s ease;
        }

        .error {
            background: #ffebee;
            color: var(--error-color);
            opacity: 1;
            transform: translateY(0);
        }

        .password-toggle {
            position: absolute;
            right: 15px;
            top: 50%;
            transform: translateY(-50%);
            cursor: pointer;
            color: #666;
            transition: color 0.3s ease;
        }

        .password-toggle:hover {
            color: var(--primary-color);
        }

        .b {
            color: #00C851;
            text-align: center;
            font-size: 1.5rem;
            font-weight: bold;
            margin-bottom: 20px;
        }

        /* Responsive Layout for Mobile (Phones) */
        @media (max-width: 600px) {
            .wrapper {
                flex-direction: column;
            }

            .image-container img {
                height: auto;
                width: 80%;
                max-width: 300px;
            }

            .container {
                padding: 1.5rem;
                max-width: 100%;
            }

            h2 {
                font-size: 1.5rem;
            }
        }
        .a{height: 10rem;
            box-shadow: inset 3px 5px 5px 1px rgba(199, 113, 1, 0.5);
            border-radius: 40%;
        }
        .loading-spinner {
            display: none;
            margin: 10px auto;
            width: 40px;
            height: 40px;
            border-radius: 50%;
            border: 4px solid transparent;
            border-top: 4px solid rgb(149, 75, 1);
            animation: spin 1s linear infinite;
        }
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        .error {
            color: red;
        }
        .success {
            color: green;
        }
    </style>
</head>
<body>


    <div class="wrapper">
        <div class="image-container">
            <img src="OPI.png" alt="Business Logo" class="a">
        </div>

        <div class="container">
            <h2><i class="fas fa-user-shield"></i> Worker Access</h2>
            <form id="loginForm" onsubmit="return handleLogin(event)">
                <div class="form-group">
                    <label for="loginUsername" style="color: rgb(0, 0, 0);"><i class="fas fa-user-tie"></i> Username</label>
                    <input type="text" id="loginUsername" placeholder="Enter admin username" style="background-color: #2c0493; color: rgb(255, 235, 235);"  required>
                </div>
                <div class="form-group" >
                    <label for="loginPassword" style="color: rgb(0, 0, 0); color: rgb(0, 0, 0)"><i class="fas fa-fingerprint"></i> Password</label>
                    <input type="password"  id="loginPassword" placeholder="Enter secure passphrase " style="background-color: #1c0494; color: rgb(255, 235, 235)"  required>
                    <i class="fas fa-eye password-toggle" onclick="togglePasswordVisibility()" style=" margin-top: 1rem;"></i>
                </div>
                <button type="submit" >Authenticate <i class="fas fa-arrow-right-to-bracket"></i></button>
                <div class="loading-spinner" id="loadingSpinner">
                                
                </div>
            </form>
            <div id="message"></div>
        </div>
    </div>

    <script>
        const ownerCredentials = {
            username: "rugero",
            password: "remy",
        };

        function togglePasswordVisibility() {
            const passwordField = document.getElementById('loginPassword');
            const icon = document.querySelector('.password-toggle');
            
            if (passwordField.type === 'password') {
                passwordField.type = 'text';
                icon.classList.replace('fa-eye', 'fa-eye-slash');
            } else {
                passwordField.type = 'password';
                icon.classList.replace('fa-eye-slash', 'fa-eye');
            }
        }

        function handleLogin(event) {
            event.preventDefault();
            const username = document.getElementById('loginUsername').value.trim();
            const password = document.getElementById('loginPassword').value.trim();
            const message = document.getElementById('message');

            if (username === ownerCredentials.username && password === ownerCredentials.password) {
                localStorage.setItem("loggedIn", "true");
                message.textContent = "Authentication successful! Redirecting...";
                message.className = 'success';
                setTimeout(() => {
                    window.location.href = "home.html";
                }, 1500);
            } else {
                message.textContent = "⚠️ Access Denied: Invalid credentials";
                message.className = 'error';
                document.getElementById('loginPassword').value = '';
                setTimeout(() => {
                    message.style.opacity = '0';
                }, 3000);
            }
        }
      

        function handleLogin(event) {
            event.preventDefault();
            const username = document.getElementById('loginUsername').value.trim();
            const password = document.getElementById('loginPassword').value.trim();
            const message = document.getElementById('message');
            const loadingSpinner = document.getElementById('loadingSpinner');

            if (username === ownerCredentials.username && password === ownerCredentials.password) {
                localStorage.setItem("loggedIn", "true");
                message.textContent = "Authentication successful! Redirecting...";
                message.className = 'success';
                loadingSpinner.style.display = 'block';

                setTimeout(() => {
                    window.location.href = "home.html";
                }, 2000);
            } else {
                message.textContent = "⚠️ Access Denied: Invalid credentials";
                message.className = 'error';
                document.getElementById('loginPassword').value = '';
                setTimeout(() => {
                    message.textContent = "";
                }, 30);
            }
        }
    </script>
</body>
</html>
