---
layout: page
title: About
permalink: /about/
---

<style>
body {font-family: 'East Sea Dokdo', cursive;
      font-size: 30px;
      margin-bottom:4px;}
</style>


<body>
  <div id="passwordPrompt" style="display: none;">
    <label for="password">Enter Password:</label>
    <input type="password" id="password">
    <button onclick="checkPassword()">Submit</button>
  </div>

  <div id="content" style="display: none;">
    <!-- Your protected content here -->
    <h1>Welcome to the secret page!</h1>
    <p>This content is only accessible with the correct password.</p>
  </div>

  <script>
    function checkPassword() {
      var password = document.getElementById('password').value;
      // Change 'your-password' to your actual password
      if (password === 'Zhang741') {
        document.getElementById('passwordPrompt').style.display = 'none';
        document.getElementById('content').style.display = 'block';
      } else {
        alert('Incorrect password. Please try again.');
      }
    }
  </script>
</body>

Hi, I am <em>**QiYuan**</em>, currently working on my Ph.D. in process control at [Nanyang Technological University](https://www.ntu.edu.sg/). I am interested in **machine learning based modeling** and **model predictive control**. When not working, I like **painting**, **photography**, and making **vlogs**. 

