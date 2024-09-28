<script>
  import { Canvas } from '@threlte/core'
  import Scene from './Scene.svelte'
</script>

<div class="main-canvas">
  <Canvas>
    <Scene />
  </Canvas>
</div>

<h1 style="color: red;"> Hello World!</h1>

<style>
	.main-canvas {
	  width: 100%;
	  height: 100%;
	  position: absolute;
	  top: 0;
	  left: 0;
	  z-index: 1;
	}
</style>
