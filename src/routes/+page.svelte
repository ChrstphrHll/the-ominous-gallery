<script lang="ts">
  import Frame from "$lib/components/Frame.svelte";

  function test(c: CanvasRenderingContext2D) {
    c.fillStyle = "red"; 
    c.fillRect(0,0,400,300); 
  }

  function test4(c:CanvasRenderingContext2D) {
    // Set line width
    c.lineWidth = 10;

    // Wall
    c.strokeRect(75, 140, 150, 110);

    // Door
    c.fillRect(130, 190, 40, 60);

    // Roof
    c.beginPath();
    c.moveTo(50, 140);
    c.lineTo(150, 60);
    c.lineTo(250, 140);
    c.closePath();
    c.stroke();
  }

  function test2(c: CanvasRenderingContext2D) {
    c.fillStyle = '#ccddff';
    c.beginPath();
    c.moveTo(50,20);
    c.lineTo(200,50);
    c.lineTo(150,80);
    c.closePath();
    c.fill();
    c.strokeStyle = 'rgb(0,128,0)';
    c.lineWidth = 5;
    c.stroke();
  }

  function test3(c: CanvasRenderingContext2D) {
    let x = 0; 
    function drawIt() { 
        window.requestAnimationFrame(drawIt); 
        c.clearRect(0,0,400,400); 
        c.fillStyle = "red"; 
        c.fillRect(x,100,200,100); 
        if (x> 400) {
          x = -400;
        } else {
          x+=5; 
        }
    } 
  
    window.requestAnimationFrame(drawIt);
  }

  const arts = [test, test2, test3, test4, test3, test3, test3, test3, test3, test3, test3, test3, test3]
</script>

<h1>The Ominous Gallery</h1>

<div class="wall">
  {#each arts as art }
    <Frame drawFn={art} />
  {/each}
</div>

<style>
  h1 {
    text-align: center;
  }

  .wall {
    display: flex;
    flex-wrap: wrap;
    gap: 16px;
    justify-content: center;
  }
</style>