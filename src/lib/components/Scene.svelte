<script>
  import { T } from '@threlte/core'
  import { ContactShadows, Float, Grid, ImageMaterial} from '@threlte/extras'
  import { onMount } from 'svelte';
    import { randInt } from 'three/src/math/MathUtils.js';
  let y = 0;

  let maxScroll = 0;

  function updateMaxScroll() {
    maxScroll = document.documentElement.scrollHeight - window.innerHeight;
  }

  onMount(() => {
    updateMaxScroll();
    window.addEventListener('resize', updateMaxScroll);
    return () => window.removeEventListener('resize', updateMaxScroll);
  });
</script>

<T.PerspectiveCamera
  makeDefault
  position={[-10, 10, 10]}
  fov={15}
  on:create={({ ref }) => {
    ref.lookAt(0, 1, 0)
  }}
/>

<T.DirectionalLight
  intensity={0.8}
  position.x={5}
  position.y={10}
/>
<T.AmbientLight intensity={0.2} />

<Grid
  position.y={-0.001}
  cellColor="#ffffff"
  sectionColor="#ffffff"
  sectionThickness={0}
  fadeDistance={25}
  cellSize={2}
/>

<ContactShadows
  scale={10}
  blur={2}
  far={2.5}
  opacity={0.5}
/>

<Float floatIntensity={0.5} floatingRange={[0,1]} speed={2}>
  <T.Mesh position={[0, 1, 0]} rotation={[randInt(0, y), randInt(0, y), randInt(0, y)]}>
    <T.BoxGeometry />
    <ImageMaterial url="/rainbowcat.jpg"/>
  </T.Mesh>
</Float>

<svelte:window bind:scrollY={y}/>