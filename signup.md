---
permalink: /signup
---
<html>
<head>
    <title>Sign Up</title>
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
        .signup-container {
            width: 300px;
            padding: 20px;
            border-radius: 8px;
            background-color: #ffffff;
            box-shadow: 0px 0px 10px 0px rgba(0,0,0,0.1); /* Add a subtle shadow effect */
        }
        .signup-container h1 {
            margin-top: 0;
            color: #333333; /* Set a darker text color for the heading */
            text-align: center;
        }
        .signup-container label {
            display: block;
            margin-bottom: 5px;
            color: #666666; /* Set a slightly darker text color for labels */
        }
        .signup-container input[type="text"],
        .signup-container input[type="password"] {
            width: 100%;
            padding: 8px;
            margin-bottom: 15px;
            border: 1px solid #cccccc;
            border-radius: 4px;
            box-sizing: border-box;
        }
        .signup-container button {
            width: 100%;
            padding: 10px;
            background-color: #007bff; /* Set a primary button color */
            border: none;
            color: #ffffff;
            border-radius: 4px;
            cursor: pointer;
        }
        .signup-container button:hover {
            background-color: #0056b3; /* Darken the button color on hover */
        }
        .signup-container .message {
            margin-top: 15px;
            text-align: center;
            color: #ff0000; /* Set a red color for error messages */
        }
        .login-button {
            width: 100%;
            padding: 10px;
            background-color: #f5f5f5; /* Set a light background color */
            border: none;
            color: #007bff; /* Set a primary button color */
            border-radius: 4px;
            cursor: pointer;
            margin-top: 10px;
        }
        .login-button a {
            text-decoration: none; /* Remove underline from the link */
            color: #ffffff;
        }
        .login-button a:hover {
            text-decoration: underline; /* Underline the link on hover */
        }
    </style>
</head>
<body>
    <div class="signup-container">
        <form action="javascript:signup_user()">
            <p><label>Name:
            <input type="text" name="name" id="name" required>
            </label></p>
            <p><label>User ID:
            <input type="text" name="uid" id="uid" required>
            </label></p>
            <p><label>
            Password:
            <input type="password" name="password" id="password" required>
            </label></p>
            <p><label>
            Date of Birth:
            <input type="date" name="dob" id="dob" required>
            </label></p>
            <p><label>
            Favorite Color:
            <input type="text" name="color" id="color" required>
            </label></p>
            <p>
            <button class="signup-button">Sign Up</button>
            </p>
        </form>
    </div>
</body>

<!-- 
Below JavaScript code is designed to handle user authentication in a web application. It's written to work with a backend server that uses JWT (JSON Web Tokens) for authentication.

The script defines a function when the page loads. This function is triggered when the Login button in the HTML form above is pressed. 
 -->
<script type="module">
    // uri variable and options object are obtained from config.js
    import { uri, options } from 'https://lin-ct.github.io/demonstration_frontend/assets/js/api/config.js';

function signup_user() {
    // Set Create User endpoint
    const url = uri + '/api/users/';

    // Set body of request to include signup data from DOM
    const body = {
        name: document.getElementById("name").value,
        uid: document.getElementById("uid").value,
        password: document.getElementById("password").value,
        dob: document.getElementById("dob").value,
        color: document.getElementById("color").value,
    };

    // Change options according to Authentication requirements
    const createOptions = {
        ...options,
        method: 'POST',
        cache: 'no-cache',
        body: JSON.stringify(body)
    };

    // Fetch to create user
    fetch(url, createOptions)
        .then(response => {
            if (!response.ok) {
                const errorMsg = 'Signup error: ' + response.status;
                console.log(errorMsg);
                alert("Error creating user");
                return;
            }

            // Success - user created
            alert("User created successfully!");
            window.location.href = "https://lin-ct.github.io/demonstration_frontend/login";
        })
        .catch(err => {
            console.error(err);
        });
}
    // Attach signup_user to the window object, allowing access to form action
    window.signup_user = signup_user;
</script>
</html>