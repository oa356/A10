<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Cookie Example</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 50px;
      background-color: #f0f0f0;
      color: #333;
    }
    .container {
      background: #fff;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
      max-width: 500px;
      margin: auto;
    }
    h1 {
      font-size: 24px;
    }
    p {
      font-size: 18px;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Cookie Demo</h1>
    <p id="cookieDisplay">Checking for cookie...</p>
  </div>

  <script>
    // Function to set a cookie with name, value and expiration days
    function setCookie(name, value, days) {
      const d = new Date();
      d.setTime(d.getTime() + (days*24*60*60*1000));
      const expires = "expires=" + d.toUTCString();
      document.cookie = name + "=" + value + ";" + expires + ";path=/";
    }

    // Function to get the value of a cookie by name
    function getCookie(name) {
      const cname = name + "=";
      const decodedCookie = decodeURIComponent(document.cookie);
      const cookieArr = decodedCookie.split(';');
      for (let i = 0; i < cookieArr.length; i++) {
        let c = cookieArr[i].trim();
        if (c.indexOf(cname) === 0) {
          return c.substring(cname.length, c.length);
        }
      }
      return "";
    }

    // On page load, check for the cookie, if not found, set it
    window.onload = function() {
      let username = getCookie("username");
      const display = document.getElementById("cookieDisplay");

      if (username !== "") {
        // If cookie exists, display it
        display.textContent = "Welcome back, " + username + "!";
      } else {
        // If cookie doesn't exist, create one
        username = "User" + Math.floor(Math.random() * 1000); // Random username
        setCookie("username", username, 7); // Cookie valid for 7 days
        display.textContent = "Cookie has been set! Reload the page.";
      }
    };
  </script>
</body>
</html>
