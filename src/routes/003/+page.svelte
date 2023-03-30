<script>
  import { onMount } from 'svelte';
  
  let canvas;
  let ctx;
  
  const PLAYER_WIDTH = 50;
  const PLAYER_HEIGHT = 30;
  
  let player;
  
  function initPlayer() {
    player = {
      x: canvas.width / 2 - PLAYER_WIDTH / 2,
      y: canvas.height - PLAYER_HEIGHT,
      speed: 5
    };
  }
  
  function drawPlayer() {
    ctx.fillStyle = '#fff'; // Set player color
    ctx.fillRect(player.x, player.y, PLAYER_WIDTH, PLAYER_HEIGHT); // Draw player rectangle
  }
  
  function movePlayer(event) {
    if (event.key === 'ArrowLeft' && player.x > 0) {
      player.x -= player.speed;
    } else if (event.key === 'ArrowRight' && player.x < canvas.width - PLAYER_WIDTH) {
      player.x += player.speed;
    }
  }
  
  function clearCanvas() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
  }
  
  function gameLoop() {
    clearCanvas();
    drawPlayer();
    requestAnimationFrame(gameLoop);
  }
  
  onMount(() => {
    canvas = document.querySelector('canvas');
    ctx = canvas.getContext('2d');
    initPlayer();
    window.addEventListener('keydown', movePlayer);
    drawPlayer();
    gameLoop();
  });
</script>

<canvas width="600" height="400"></canvas>
