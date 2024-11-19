<script>
  import { Canvas } from '@threlte/core';
  import Scene from './Scene.svelte';
</script>

<section>
  <div id="canvas">
    <Canvas>
      <Scene />
    </Canvas>
  </div>

  <div id="canvas-overlay">
    <p style="color: red;">This is my scene!</p>
  </div>
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
