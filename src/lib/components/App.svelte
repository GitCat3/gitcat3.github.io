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

<section>
  <div id="canvas">
    <Canvas>
      <Scene />
    </Canvas>
  </div>

  {#if showOverlay}
    <div id="canvas-overlay" in:fade={{ duration: 2000, delay: 2000 }}>
      <p style="color: red;">This is my scene!</p>
    </div>
  {/if}
</section>

<style lang="scss">
  section {
    position: relative;
    width: 100vw;
    height: 100vh;
    #canvas-overlay {
      position: absolute;
      top: 10%;
      left: 10%;
      transform: translate(-50%, -50%);
      color: red;
    }
    #canvas {
      width: 100%;
      height: 100%;
      display: block;
    }
}
</style>
