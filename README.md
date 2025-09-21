<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Combat Tower - Official Website</title>
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }
    body {
      font-family: 'Trebuchet MS', sans-serif;
      background: linear-gradient(135deg, #ffcc00, #ff8800);
      color: #fff;
      overflow-x: hidden;
    }
    header {
      position: relative;
      text-align: center;
      padding: 80px 20px;
      background: rgba(0,0,0,0.6);
      overflow: hidden;
    }
    header h1 {
      font-size: 3rem;
      text-shadow: 0 0 5px #ff0000, 0 0 10px #ff8800, 0 0 20px #ffcc00;
      animation: glow 1.5s infinite alternate;
      position: relative;
      z-index: 2;
    }
    header p {
      font-size: 1.2rem;
      margin-top: 10px;
      opacity: 0.9;
      position: relative;
      z-index: 2;
    }
    @keyframes glow {
      from { text-shadow: 0 0 5px #ff0000, 0 0 10px #ff8800, 0 0 20px #ffcc00; }
      to { text-shadow: 0 0 10px #ff0000, 0 0 20px #ff8800, 0 0 40px #ffcc00; }
    }
    #sparkCanvas { position: absolute; top: 0; left: 0; width: 100%; height: 100%; z-index: 1; pointer-events: none; }

    nav { display: flex; justify-content: center; background: rgba(0,0,0,0.8); position: sticky; top: 0; z-index: 10; }
    nav a { color: #fff; text-decoration: none; padding: 14px 25px; display: block; transition: 0.3s; font-weight: bold; }
    nav a:hover { background: #ffcc00; color: #000; box-shadow: 0 4px 10px rgba(0,0,0,0.4); }

    .container { padding: 60px 20px; text-align: center; animation: fadeInUp 1.5s ease; }
    .button {
      background: #ff8800; color: white; padding: 15px 30px; text-decoration: none;
      border-radius: 12px; margin: 10px; display: inline-block; font-size: 1.1rem;
      font-weight: bold; transition: all 0.3s ease; box-shadow: 0 4px 10px rgba(0,0,0,0.4);
    }
    .button:hover { background: #ffcc00; color: #000; transform: scale(1.05); }

    .gamepass-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); gap: 20px; margin-top: 20px; }
    .card {
      background: rgba(0,0,0,0.7); border-radius: 15px; padding: 20px; transition: 0.3s;
      box-shadow: 0 4px 12px rgba(0,0,0,0.5);
    }
    .card:hover { transform: translateY(-8px); background: rgba(0,0,0,0.9); }
    .card h3 { margin-bottom: 10px; }

    footer { background: rgba(0,0,0,0.8); color: #ccc; text-align: center; padding: 20px; margin-top: 40px; font-size: 0.9rem; }

    @keyframes fadeInDown { from { opacity: 0; transform: translateY(-30px); } to { opacity: 1; transform: translateY(0); } }
    @keyframes fadeInUp { from { opacity: 0; transform: translateY(30px); } to { opacity: 1; transform: translateY(0); } }

  </style>
</head>
<body>
  <header>
    <div class="header-content">
      <h1>👊 Combat Tower 👊</h1>
      <p>The official website of Combat Tower — climb, slap, and conquer!</p>
    </div>
    <canvas id="sparkCanvas"></canvas>
  </header>

  <nav>
    <a href="#home">Home</a>
    <a href="#play">Play</a>
    <a href="#gamepasses">Gamepasses</a>
    <a href="#updates">Updates</a>
  </nav>

  <div id="home" class="container">
    <h2>Welcome!</h2>
    <p>Climb your way to victory! Join thousands of players in the funniest tower combat on Roblox.</p>
  </div>

  <div id="play" class="container">
    <h2>Play the Game</h2>
    <a class="button" href="https://www.roblox.com/games/12168261951/Combat-Tower" target="_blank">▶️ Play on Roblox</a>
  </div>

  <div id="gamepasses" class="container">
    <h2>Gamepasses</h2>
    <div class="gamepass-grid">
      <div class="card">
        <h3>🖐️ Giant Slap</h3>
        <a class="button" href="https://www.roblox.com/game-pass/847246159" target="_blank">Buy Now</a>
      </div>
      <div class="card">
        <h3>🌈 Rainbow Slap</h3>
        <a class="button" href="https://www.roblox.com/game-pass/842690114" target="_blank">Buy Now</a>
      </div>
      <div class="card">
        <h3>🔫 Mini Gun</h3>
        <a class="button" href="https://www.roblox.com/game-pass/842618520" target="_blank">Buy Now</a>
      </div>
      <div class="card">
        <h3>⏳ Time Slap</h3>
        <a class="button" href="https://www.roblox.com/game-pass/705483741" target="_blank">Buy Now</a>
      </div>
      <div class="card">
        <h3>🪄 Magic Carpet</h3>
        <a class="button" href="https://www.roblox.com/game-pass/705677378" target="_blank">Buy Now</a>
      </div>
      <div class="card">
        <h3>⚙️ HD Admin</h3>
        <a class="button" href="https://www.roblox.com/game-pass/846961908" target="_blank">Buy Now</a>
      </div>
    </div>
  </div>

  <div id="updates" class="container">
    <h2>Latest Updates</h2>
    <p>🔥 New slap powers and bug fixes!</p>
    <p>⚡ Improved performance for smoother gameplay.</p>
  </div>

  <footer>
    <p>&copy; 2025 Combat Tower | Not affiliated with Roblox Corporation</p>
  </footer>

  <script>
    const canvas = document.getElementById('sparkCanvas');
    const ctx = canvas.getContext('2d');
    const header = document.querySelector('header');
    canvas.width = window.innerWidth;
    canvas.height = header.offsetHeight;

    class Spark {
      constructor() { this.reset(); }
      reset() {
        this.x = Math.random() * canvas.width;
        this.y = canvas.height + Math.random() * 50;
        this.size = Math.random() * 3 + 1;
        this.speedY = Math.random() * 2 + 1;
        this.color = ['#ff0000','#ff8800','#ffcc00'][Math.floor(Math.random()*3)];
      }
      update() { this.y -= this.speedY; if(this.y < 0) this.reset(); }
      draw() { ctx.beginPath(); ctx.arc(this.x,this.y,this.size,0,Math.PI*2); ctx.fillStyle = this.color; ctx.fill(); }
    }
    const sparks = Array.from({length:50},()=>new Spark());

    class SwordSlash {
      constructor() { this.reset(); }
      reset() {
        this.x = -100;
        this.y = Math.random() * canvas.height;
        this.angle = (Math.random() * 50 - 25) * Math.PI / 180;
        this.length = 60 + Math.random() * 40;
        this.speed = 5 + Math.random() * 3;
        this.opacity = 0;
        this.fadeIn = true;
      }
      update() {
        this.x += this.speed;
        if(this.fadeIn){ this.opacity += 0.05; if(this.opacity >= 0.8) this.fadeIn=false; }
        else { this.opacity -= 0.02; }
        if(this.x > canvas.width + 100 || this.opacity <= 0) this.reset();
      }
      draw() {
        ctx.save();
        ctx.translate(this.x,this.y);
        ctx.rotate(this.angle);
        ctx.globalAlpha = this.opacity;
        ctx.fillStyle = '#fff';
        ctx.fillRect(0,0,this.length,8);
        ctx.restore();
        ctx.globalAlpha = 1;
      }
    }
    const swords = Array.from({length:8},()=>new SwordSlash());

    function animateHeader(){
      ctx.clearRect(0,0,canvas.width,canvas.height);
      sparks.forEach(s=>{s.update(); s.draw();});
      swords.forEach(s=>{s.update(); s.draw();});
      requestAnimationFrame(animateHeader);
    }
    animateHeader();

    window.addEventListener('resize',()=>{
      canvas.width = window.innerWidth;
      canvas.height = header.offsetHeight;
    });
  </script>
</body>
</html>
