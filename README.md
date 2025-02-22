<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Secure Login</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    <style>
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background: #f4f4f4;
        }
        .container {
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            text-align: center;
        }
        .loading-spinner {
            display: none;
            margin: 10px auto;
            width: 40px;
            height: 40px;
            border-radius: 50%;
            border: 4px solid transparent;
            border-top: 4px solid blue;
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
    <div class="container">
        <h2>Login</h2>
        <form id="loginForm" onsubmit="return handleLogin(event)">
            <input type="text" id="loginUsername" placeholder="Username" required><br><br>
            <input type="password" id="loginPassword" placeholder="Password" required><br><br>
            <button type="submit">Login</button>
            <div class="loading-spinner" id="loadingSpinner"></div>
        </form>
        <div id="message"></div>
    </div>

  
</body>
</html>
