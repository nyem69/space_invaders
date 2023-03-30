<script>
  import { onMount } from 'svelte';
  
  let canvas;
  
  function createGameBoard() {
    const ctx = canvas.getContext('2d');
    ctx.fillStyle = '#000'; // Set background color
    ctx.fillRect(0, 0, canvas.width, canvas.height); // Fill canvas with color
  }
  
  onMount(() => {
    createGameBoard();
  });
</script>

<canvas bind:this={canvas} width="600" height="400"></canvas>
