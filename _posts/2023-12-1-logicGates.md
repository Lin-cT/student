---
toc: True
comments: True
layout: post
title: Logic Gates 
description: This door game employs logic gates to teach about binary. Above the keypads, there are hints on what button to click, and also the logical operator the keypad is using. When a button is clicked, the assigned value (the default assigned value is 0 for off) becomes 1 (for on). Using the hints, determine what value the buttons must have (0 or 1, off or on) in order to fufill the requirements for each keypad and pass to the next level. 
courses: {'compsci': {'week': 17}}
type: tangibles
permalink: "lg"
---
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>

<body>
    <div class="main-container">
        <div class="door-lightbulb-container">
            <img src="off_lightbulb.png" id="lightbulb">
            <img src="door1.png" id="door1">
        </div>
        <div class="text-buttons">
        <img src="and.png" id="and">
        <p id="text1">Click on button 1 AND button 2.</p>
        <div class="button-container2">
          <button class="my-button" id="b1" onclick="toggle1Value(this);">1</button>
          <button class="my-button" id="b2" onclick="toggle2Value(this);">2</button>
        </div>
        <br>
        <img src="or.png" id="or">
        <p id="text2">Click on button 1 OR button 2, OR both!</p>
        <div class="button-container2">
          <button class="my-button" id="b7" onclick="toggle7Value(this);">1</button>
          <button class="my-button" id="b8" onclick="toggle8Value(this);">2</button>
        </div>
        <button id="check" onclick="checkAnswer()">Check!</button>
        <button id="enter" onclick="clickEnter()" style="display: none;">Enter!</button>
        <button id="check2" onclick="checkAnswer2()" style="display: none;">Check!</button>
      </div>
    </div>
    <div id="level-container">
    </div>
  </body>
  <script>
  // Variable to keep track of the button value
  var button1Value = 0;
  var button2Value = 0;
  var button7Value = 0;
  var button8Value = 0;
  // Function to toggle the button value
  function toggle1Value(button) {
    // Toggle between 0 and 1
    button1Value = 1 - button1Value;
    changeColor(button);
  }
  // Function to toggle the button value
  function toggle2Value(button) {
    // Toggle between 0 and 1
    button2Value = 1 - button2Value;
    changeColor(button);
  }
    // Function to toggle the button value
  function toggle7Value(button) {
    // Toggle between 0 and 1
    button7Value = 1 - button7Value;
    changeColor(button);
  }
  // Function to toggle the button value
  function toggle8Value(button) {
    // Toggle between 0 and 1
    button8Value = 1 - button8Value;
    changeColor(button);
  }
  function openDoor() {
    var doorImage = document.getElementById('door1')
    doorImage.src = 'door1_Open.png';
    doorImage.alt = 'Open Door';
  }
  function correctAnswer() {
    var correctAnswer = false
    if (button1Value === 1 && button2Value === 1 && button8Value === 1 || button7Value === 1) {
      return correctAnswer = true
    }
    else {
      return correctAnswer = false
    }
  }
  function correctAnswer2() {
    var correctAnswer = false
    if (button1Value !== 1 && ((button7Value === 1) !== (button8Value === 1))) {
      correctAnswer = true;
      return correctAnswer = true
    }
    else {
      return correctAnswer = false
    }
  }
function changeColor(button) {
    var defaultColor = '#808080'; // Replace with the default color of your buttons
    if (button.style.backgroundColor === 'blue') {
        button.style.backgroundColor = defaultColor; // Reset to default color
    } else {
        button.style.backgroundColor = 'blue';
    }
}
function checkAnswer() {
    if (correctAnswer()) {
        var lightbulb = document.getElementById('lightbulb');
        lightbulb.src = 'on_lightbulb.png'; // Fix the line
        openDoor();
        alert("Correct! You can move on to the next level.");
        document.getElementById('enter').style.display = 'block'; // Show the "Enter" button
    } else {
        alert("Incorrect answer. Try again!");
    }
}
function checkAnswer2() {
  if (correctAnswer2()) {
    var lightbulb = document.getElementById('lightbulb')
    lightbulb.src = 'on_lightbulb.png';
    openDoor();
    alert("Correct! Congrats!");
  } else {
      alert("Incorrect answer. Try again!");
    }
}
function clickEnter() {
    // Update questions and choices
    var door = document.getElementById('door1')
    var andImage = document.getElementById('and');
    var orImage = document.getElementById('or');
    var lightbulb = document.getElementById('lightbulb')
    door.src = 'door1.png';
    lightbulb.src = 'off_lightbulb.png';
    andImage.src = 'not.png'; // Replace with the path to your nor gate image
    orImage.src = 'xor.png'; // Replace with the path to your not gate image
    // Hide the "Enter" button after clicking
    document.getElementById('enter').style.display = 'none';
    document.getElementById('check').style.display = 'none';
    document.getElementById('check2').style.display = 'block';
    button1Value = 0;
    button2Value = 0;
    button7Value = 0;
    button8Value = 0;
    var b1 = document.getElementById("b1");
    var b2 = document.getElementById("b2");
    var b7 = document.getElementById("b7");
    var b8 = document.getElementById("b8");
    var text1 = document.getElementById("text1");
    var text2 = document.getElementById("text2");
    text1.innerHTML = "Do NOT click on the 1st button.";
    b1.style.backgroundColor = "";
    b2.style.backgroundColor = "";
    text2.innerHTML = "Click on button 1 OR button 2, but NOT both!";
    b7.innerHTML = "1";
    b8.innerHTML = "2";
    b7.style.backgroundColor = "";
    b8.style.backgroundColor = "";
}

</script>