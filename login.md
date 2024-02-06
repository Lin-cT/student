---
permalink: /login
---

<html>
<head>
    <title>Login</title>
    <style>
        body {
            background-color: #f5f5f5; /* Set a light background color */
            font-family: Arial, sans-serif; /* Set a common font family */
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }
        .login-container {
            width: 300px;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0px 0px 10px 0px rgba(0,0,0,0.1); /* Add a subtle shadow effect */
        }
        .login-container h1 {
            margin-top: 0;
            color: #333333; /* Set a darker text color for the heading */
            text-align: center;
        }
        .login-container label {
            display: block;
            margin-bottom: 5px;
            color: #666666; /* Set a slightly darker text color for labels */
        }
        .login-container input[type="text"],
        .login-container input[type="password"] {
            width: 100%;
            padding: 8px;
            margin-bottom: 15px;
            border: 1px solid #cccccc;
            border-radius: 4px;
            box-sizing: border-box;
        }
        .login-container button {
            width: 100%;
            padding: 10px;
            background-color: #007bff; /* Set a primary button color */
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }
        .login-container button:hover {
            background-color: #0056b3; /* Darken the button color on hover */
        }
        .login-container .message {
            margin-top: 15px;
            text-align: center;
            color: #ff0000; /* Set a red color for error messages */
        }
    </style>
</head>
<body>
    <div class="login-container">
        <h1>Login</h1>
        <form id="loginForm">
            <label for="uid">Username:</label>
            <input type="text" id="uid" name="username" required>
            <br>
            <label for="password">Password:</label>
            <input type="password" id="password" name="password" required>
            <br>
            <button type="button" onclick="login()">Login</button>
        </form>
        <div id="output" class="message"></div>
        <br>
        <a id="signup" href="https://lin-ct.github.io/demonstration_frontend/signup.html">Log In</a>
    </div>
</body>
<script>
       function login(){
        console.log("Starting!")
        // Set Authenticate endpoint
        const url = 'http://127.0.0.1:8086/api/users/authenticate';
        console.log("Getting body.")
        // Set the body of the request to include login data from the DOM
        const body = {
            uid: document.getElementById("uid").value,
            password: document.getElementById("password").value,
        };
        // Change options according to Authentication requirements
        const authOptions = {
            mode: 'cors', // no-cors, *cors, same-origin
            credentials: 'include', // include, same-origin, omit
            headers: {
                'Content-Type': 'application/json',
            },
            method: 'POST', // Override the method property
            cache: 'no-cache', // Set the cache property
            body: JSON.stringify(body)
        };
        // Fetch JWT
        fetch(url, authOptions)
        .then(response => {
            // handle error response from Web API
            if (!response.ok) {
                error = document.getElementById("output")
                const errorMsg = 'Login error: ' + response.status;
                console.log(errorMsg);
                alert("Failed Authentication: Credentials Incorrect")
                error.innerHTML = errorMsg
                return;
            }
            // Success!!!
            // Redirect to the database page
            window.location.href = "https://lin-ct.github.io/demonstration_frontend/CRUD.html";
        })
        // catch fetch errors (ie ACCESS to server blocked)
        .catch(err => {
            console.error(err);
        });
    }
    window.login_user = login_user;
</script>
</html>