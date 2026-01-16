<script lang="ts">
  import { onMount } from "svelte";

  let { drawFn } = $props();

  let canvas: HTMLCanvasElement | undefined;
  let ctx: CanvasRenderingContext2D | null;


  onMount(() => {
    if(!canvas) {
      return
    }
    ctx = canvas.getContext("2d");

    if (ctx) {
      drawFn(ctx)
    }
  })

</script>

<div class="frame-backing">
  <canvas bind:this={canvas}></canvas>
</div>

<style>
  canvas {
    width: 300px;
    height: 300px;
    border: red solid 3px;
    display: block;

    --frame-depth: 20px;

    border-image-slice:71 71 71 71;
    border-image-width: var(--frame-depth) var(--frame-depth) var(--frame-depth) var(--frame-depth);
    border-image-outset: var(--frame-depth) var(--frame-depth) var(--frame-depth) var(--frame-depth);
    border-image-repeat:round round;
    border-image-source:url("frame.png");
    border-style: solid;
    margin: var(--frame-depth);
  }

  .frame-backing {
    background-color: antiquewhite;
    height: min-content;
    box-shadow: 0px 5px 22px -7px rgba(0, 0, 0, 0.90);
  }
</style>