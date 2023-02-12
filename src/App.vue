<script setup>
 import axios from "axios";

const options = {
  method: 'GET',
  url: 'https://roll-dice1.p.rapidapi.com/rollDice',
  headers: {
    'X-RapidAPI-Key': '22426d6286mshf6c1a6c3be16aedp14f912jsn29e470560d4e',
    'X-RapidAPI-Host': 'roll-dice1.p.rapidapi.com'
  }
};

axios.request(options).then(function (response) {
	console.log(response.data);
}).catch(function (error) {
	console.error(error);
});

let images = ["dice-01.svg",
"dice-02.svg",
"dice-03.svg",
"dice-04.svg",
"dice-05.svg",
"dice-06.svg"];
let dice = document.querySelectorAll("img");

function roll(){
    dice.forEach(function(die){
        die.classList.add("shake");
    });
    setTimeout(function(){
        dice.forEach(function(die){
            die.classList.remove("shake");
        });
        let dieOneValue = Math.floor(Math.random()*6);
        let dieTwoValue = Math.floor(Math.random()*6);
        console.log(dieOneValue,dieTwoValue);
        document.querySelector("#die-1").setAttribute("src", images[dieOneValue]);
        document.querySelector("#die-2").setAttribute("src", images[dieTwoValue]);
        document.querySelector("#total").innerHTML = "Your roll is " + ( (dieOneValue +1) + (dieTwoValue + 1) );
    },
    1000
    );
}
roll();

</script>



<template>
  <head>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@500&display=swap" rel="stylesheet">
    
    <link rel="stylesheet" href="style.css">
</head>
<body>
<div class="container">
        <div class="dice-wrapper">
            <img  id="die-1">
            <img  id="die-2">
        </div>
        <p id="total"></p>
        <button @click="roll">ROLL THE DICE</button>
    </div>
  </body>
    

</template>

<style>


body{
  height: 100vh;
  background: linear-gradient(
      #e92e3d,
      #ff6e6a
  ) 0 100% no-repeat;
  background-size: 100% 50%;
}
.container{
  width: 400px;
  padding: 50px;
  position: absolute;
  transform: translate(-50%,-50%);
  top: 50%;
  left: 50%;
  background-color: #ffffff;
  box-shadow: 0 15px 25px rgba(50,50,50,0.15);
  border-radius: 8px;
  display: flex;
  flex-direction: column;
  align-items: center;
  font-family: "Poppins",sans-serif;
}
.dice-wrapper{
  width: 90%;
  display: flex;
  justify-content: space-around;
}
p{
  font-size: 16px;
  margin: 30px 0;
  font-weight: 500;
}
button{
  background-color: #e92e3d;
  border: none;
  outline: none;
  color: #ffffff;
  padding: 15px 0;
  width: 150px;
  letter-spacing: 1px;
  border-radius: 5px;
  cursor: pointer;
}
.shake{
  animation: shake 0.5s infinite;
}
@keyframes shake{
  0%{
      transform: rotate(8deg);
  }
  50%{
      transform: rotate(-8deg);
  }
  100%{
      transform: rotate(8deg);
  }
}

</style>