<script>
  import { Canvas } from '@threlte/core';
  import Scene from './Scene.svelte';
  import { fade } from 'svelte/transition';
  import { onMount } from 'svelte';
  let showOverlay = false;
  onMount(() => {
    showOverlay = true;
  });
</script>
<head>
  <link href="https://fonts.googleapis.com/css2?family=Lato:ital,wght@0,100;0,300;0,400;0,700;0,900;1,100;1,300;1,400;1,700;1,900&display=swap" rel="stylesheet">
</head>

<section>
  <div id="canvas">
    <Canvas>
      <Scene />
    </Canvas>
  </div>

  {#if showOverlay}
    <div id="canvas-overlay1" in:fade={{ duration: 2000, delay: 2000 }}>
      <p style="color: white; font-size: 40px; font-family: Lato, serif;">This is my scene!</p>
    </div>
  {/if}
  <div id="canvas-overlay2">
    <a href="https://github.com/GitCat3/" target="_blank" rel="noopener noreferrer">
      <img src="github.png" alt="GitCat3's Github page" width=64 height=64 style="transition: transform 0.3s ease;"/>
    </a>
  </div>
</section>

<style lang="scss">
  section {
    position: relative;
    width: 100vw;
    height: 100vh;
    #canvas-overlay1 {
      position: absolute;
      top: 10%;
      left: 50%;
      transform: translate(-50%, -50%);
    }
    #canvas-overlay2 {
      position: absolute;
      top: 95%;
      left: 95%;
      transform: translate(-50%, -50%);
        img:hover {
          transform: scale(1.2);
        }
    }
    #canvas {
      width: 100%;
      height: 100%;
      display: block;
    }
}
</style>
