<html>

<head>

		<title>The Idle Stoner </title>
		
		<style>
		
		.sectionLeft {
			float: left;
			width: 80%;
			
		}
			
		.sectionRight {	
			float: right;
			width: 20%;
	
		}
		
		.scoreContainer {
				background-color: rgb(92, 41, 74, 0.6);
				width: 50%;
				padding: 10px;
				border-radius: 10px;
				font-size: 24px;
				font-weight: bold;
		
		}
		
		
		.clickerContainer img {
			position: relative;
			transition: all .2s ease-in-out;
	
		}
		
		.clickerContainer img:hover { transform: scale(1.10); }
		.clickerContainer img:active { transform: scale(0.99); }
		
		
		
		
		.shopButton {
			background-color:rgb(92, 41, 74, 0.6);
			transition: all .2s ease-in-out;
			border-radius: 10px;
			width: 100%;
			margin: 10px 0px 10px 10px;
		
		}
		
		.shopButton:hover {
			background-color: lightpink;
			transition: all .2s ease-in-out;
			
			
		}	
		
		
		.shoButton #image {
			width:25%;
		}


		.shopButton img {
			height: 64px;
			width:	64px;
			
			
		}	
		
		
		.shopButton #nameAndCost p {
			margin: 0px;
			width: 60%; 
		
		}
		
		
		.shopButton #nameAndCost p:first-of-type {
			font-size: 24px;
		
		
		}
		
		.shopButton #amount {
			font-size: 48px;
			color: purple;
			font-family: roboto;
			width: 15%;	
		
		
		}
		
		.sectionFooter {
			margin-top: 20%;
			
		
		}
		
		.unselectable {
			user-select:none;
		
		}
			
		
		
		
		</style>

</head>


	<body>
		<div class="sectionLeft">
		
			<center>
				<div class="scoreContainer unselectable">
					<span id="score">0</span> weedcrumbs<br>
					<span id="scorePerSecond">0</span> weedcrumbs per second
				</div>
				<br>
				<div class="clickerContainer unselectable">
					<img src="images/nugget100px.png" height="256px" width="256px" onclick="addToScore(clickingPower)">
				</div>
				<br>
				<button onclick="saveGame();">Save Game</button>
				<button onclick="loadGame();">Load Game</button>
			</center>

			<div class="sectionFooter">
				<h5> The Idle Stoner </h5>
			</div>				
		</div>
		
		<div class="sectionRight">
			<table class="shopButton unselectable" onclick="buyBuzzer()">
				<tr>
					<td id="image"><img src="images/bumblebee32px-fixed.png"></td>
					<td id="nameAndCost">
						<p>Buzzer <span id="buzzercost">15</span> weecrumbs </p>
					</td>
					<td id="amount"><span id="buzzers">0</span></td>
				</tr>
			
			</table>
			
				<table class="shopButton unselectable" onclick="buyPothog()">
				<tr>
					<td id="image"><img src="images/pothog32px.png">
					<td id="nameAndCost">
						<p>Pothog <span id="pothogcost">100</span> weecrumbs </p>
					</td>
					<td id="amount"><span id="pothogs">0</span></td>
				</tr>
			</table>
			
			<table class="shopButton" onclick="buyCannacat()">
				<tr>
					<td id="image"><img src="images/cannacat32px.png">
					<td id="nameAndCost">
						<p>Cannacat <span id="cannacatcost">1000</span> weecrumbs </p>
					</td>
					<td id="amount"><span id="cannacats">0</span></td>
				</tr>
			</table>
	
		</div>
		
			<script>
				var score = 0;
				var scorePerSecond = buzzers + pothogs * 5;
				var clickingPower = 1;
			
				var buzzerCost = 15;
				var buzzers = 0;
			
				var pothogCost = 100;
				var pothogs = 0;
				
				var cannacatCost = 1000;
				var cannacats = 0;
			
			
				function buyBuzzer() {
					if (score >= buzzerCost) {
					score = score - buzzerCost;
					buzzers = buzzers + 1;
					buzzerCost = Math.round(buzzerCost * 1.15);
				
					document.getElementById("score").innerHTML = score;
					document.getElementById("buzzercost").innerHTML = buzzerCost;
					document.getElementById("buzzers").innerHTML = buzzers;
					updateScorePerSecond();
				
					}
					
				}	
				
			
				function buyPothog() {
					if (score >= pothogCost) {
					score = score - pothogCost;
					pothogs = pothogs + 1;
					pothogCost = Math.round(pothogCost * 1.15);
					
					document.getElementById("score").innerHTML = score;
					document.getElementById("pothogcost").innerHTML = pothogCost;
					document.getElementById("pothogs").innerHTML = pothogs;
					updateScorePerSecond();
					
					}
				
				}
				
				
				function buyCannacat() {
					if (score >= cannacatCost) {
					score = score - cannacatCost;
					cannacats = cannacats + 1;
					cannacatCost = Math.round(cannacatCost * 1.15);
				
					document.getElementById("score").innerHTML = score;
					document.getElementById("cannacatcost").innerHTML = cannacatCost;
					document.getElementById("cannacats").innerHTML = cannacats;
					updateScorePerSecond();
				
					}
					
				}	
				
				function addToScore(amount) {
					score = score + amount;
					document.getElementById("score").innerHTML = score;
					
				}
			
				function updateScorePerSecond() {
					scorePerSecond = buzzers + pothogs * 5 + cannacats * 70;
					document.getElementById("scorePerSecond").innerHTML = scorePerSecond;
				}
			
			
				function saveGame() {
					var gameSave = {
					score:  score,
					clickingPower: clickingPower,
					buzzerCost: buzzerCost,
					buzzers: buzzers,
					pothogCost: pothogCost,
					pothogs: pothogs,
					cannacatCost: cannacatCost,
					cannacats: cannacats
					
					};
					localStorage.setItem("gameSave", JSON.stringify(gameSave));
					
					
				function loadGame() {
				var savedGame = JSON.parse(localStorage.getItem("gamesave"));	
				
				}
			
				setInterval(function() {
					score = score + buzzers;
					score = score + pothogs * 5;
					score = score + cannacats *70;
					document.getElementById("score").innerHTML = score;
				}, 1000); // 1000ms = 1 second
				
				document.title = score + " weedcrumbs - The Idle Stoner";
				
				
				setInterval (function)) {
					saveGame();
				
				}, 30000); //30000ms = 30 seconds
	
			</script>
			
			
			<!-- The core Firebase JS SDK is always required and must be listed first -->
			<script src="/__/firebase/8.7.1/firebase-app.js"></script>	

			<!-- TODO: Add SDKs for Firebase products that you want to use
				https://firebase.google.com/docs/web/setup#available-libraries -->
			<script src="/__/firebase/8.7.1/firebase-analytics.js"></script>

			<!-- Initialize Firebase -->
			<script src="/__/firebase/init.js"></script>	
	
			
			<script>
				function {
					var admin = require("firebase-admin")
				
					var serviceAccount = require("path/to/serviceAccountKey.json");
				
					admin.initializeApp({
						credential: admin.credential.cert(serviceAccount)			
					});
			
			}
			</script>
	</body>

</html>