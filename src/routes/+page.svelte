<script>
  import { onMount } from 'svelte';
  
  let canvas;
  let ctx;

  let width = 600;
  let height = 400;

  function createGameBoard() {
    const ctx = canvas.getContext('2d');
    ctx.fillStyle = '#000'; // Set background color
    ctx.fillRect(0, 0, canvas.width, canvas.height); // Fill canvas with color
  }
  
  function redrawGameBoard() {
    ctx.fillStyle = '#000'; // Set background color
    ctx.fillRect(0, 0, canvas.width, canvas.height); // Fill canvas with color
  }

  const PLAYER_WIDTH = 50;
  const PLAYER_HEIGHT = 30;
  

  // let player = {
  //   x: canvas.width / 2 - PLAYER_WIDTH / 2,
  //   y: canvas.height - PLAYER_HEIGHT,
  //   speed: 5
  // };

  let player = {};

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
    drawPlayer(); // Redraw player on each movement
  }
  

  function clearCanvas() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
  }
  
  function gameLoop() {

    //clearCanvas();
    redrawGameBoard();

    drawPlayer();
    requestAnimationFrame(gameLoop);
  }

  onMount(() => {
    canvas = document.querySelector('canvas');
    ctx = canvas.getContext('2d');

    console.log('canvas.width', canvas.width);

    player.x =  canvas.width / 2 - PLAYER_WIDTH / 2;
    player.y =  canvas.height - PLAYER_HEIGHT;
    player.speed = 20;

    createGameBoard();
    drawPlayer();

    gameLoop();

    // window.addEventListener('keydown', movePlayer);

  });
</script>

<canvas bind:this={canvas} width="{width}" height="{height}"></canvas>
<svelte:window on:keydown={movePlayer}/>








