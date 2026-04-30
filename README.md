# Moite-Clicker <!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Moite Clicker</title>

<style>
  body {
    margin: 0;
    font-family: Arial, sans-serif;
    background: linear-gradient(180deg, #111, #1c1c1c);
    color: white;
    text-align: center;
  }

  h1 {
    margin-top: 20px;
    font-size: 2.5rem;
  }

  #score {
    font-size: 2rem;
    margin: 10px 0;
  }

  #mps {
    font-size: 1rem;
    opacity: 0.8;
  }

  .moite-img {
    width: 260px;
    border-radius: 50%;
    cursor: pointer;
    transition: transform 0.1s, box-shadow 0.2s;
  }

  .moite-img:hover {
    box-shadow: 0 0 25px rgba(255,255,255,0.2);
  }

  .moite-img:active {
    transform: scale(0.9);
  }

  .container {
    margin-top: 30px;
  }

  .shop {
    margin-top: 40px;
  }

  button {
    padding: 12px 20px;
    margin: 10px;
    font-size: 1rem;
    border: none;
    border-radius: 8px;
    background: #ff4757;
    color: white;
    cursor: pointer;
  }

  button:hover {
    background: #ff6b81;
  }
</style>
</head>

<body>

<h1>Moite Clicker</h1>

<div id="score">Moites: 0</div>
<div id="mps">Per second: 0</div>

<div class="container">
  <!-- IMAGE EMBEDDED HERE -->
  <img class="moite-img" onclick="clickMoite()" src="data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD...(truncated)">
</div>

<div class="shop">
  <button onclick="buyAuto()">Buy Auto Clicker (+1/sec) | Cost: <span id="cost">50</span></button>
</div>

<script>
let moites = 0;
let mps = 0;
let cost = 50;

// LOAD SAVE
if (localStorage.getItem("moiteSave")) {
  let save = JSON.parse(localStorage.getItem("moiteSave"));
  moites = save.moites;
  mps = save.mps;
  cost = save.cost;
}

// CLICK
function clickMoite() {
  moites += 1;
  update();
}

// AUTO CLICK
setInterval(() => {
  moites += mps;
  update();
}, 1000);

// BUY UPGRADE
function buyAuto() {
  if (moites >= cost) {
    moites -= cost;
    mps += 1;
    cost = Math.floor(cost * 1.5);
    update();
  }
}

// UPDATE UI
function update() {
  document.getElementById("score").innerText = "Moites: " + moites;
  document.getElementById("mps").innerText = "Per second: " + mps;
  document.getElementById("cost").innerText = cost;

  // SAVE
  localStorage.setItem("moiteSave", JSON.stringify({
    moites: moites,
    mps: mps,
    cost: cost
  }));
}

// INITIAL UPDATE
update();
</script>

</body>
</html>