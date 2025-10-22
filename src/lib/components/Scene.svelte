<script>
  import { T } from '@threlte/core'
  import { ContactShadows, Float, Grid, ImageMaterial, Text3DGeometry} from '@threlte/extras'
  import { onMount } from 'svelte';
  let y = 0;

  let maxScroll = 0;
  /** @type {any} */
  let cameraRef;

  const radius = Math.sqrt(10 * 10 + 10 * 10);
  const orbitHeight = 10;

  $: if (cameraRef && y >= 0) {
    // Calculate maxScroll dynamically on each scroll update
    const currentMaxScroll = document.documentElement.scrollHeight - window.innerHeight;
    const scrollProgress = currentMaxScroll > 0 ? y / currentMaxScroll : 0;
    const angle = scrollProgress * Math.PI * 2;
    
    cameraRef.position.x = Math.cos(angle) * radius;
    cameraRef.position.z = Math.sin(angle) * radius;
    cameraRef.position.y = orbitHeight;
    cameraRef.lookAt(0, 1.5, 0);
  }
</script>

<T.PerspectiveCamera
  makeDefault
  position={[-10, 10, 10]}
  fov={15}
  on:create={({ ref }) => {
    cameraRef = ref;
    ref.lookAt(0, 1.5, 0);
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

<T.Mesh position={[0, 2.1, 1.2]} rotation={[0, Math.PI/2, 0]}>
  <Text3DGeometry 
    text="GitCat3"
    size={0.5}
    height={0.1}
  />
  <T.MeshStandardMaterial color="#ff0000" />
</T.Mesh>

<Float floatIntensity={0.5} floatingRange={[0,1]} speed={2}>
  <T.Mesh position={[0, 1, 0]}>
    <T.BoxGeometry />
    <ImageMaterial url="/rainbowcat.jpg"/>
  </T.Mesh>
</Float>

<svelte:window bind:scrollY={y} on:click={() => console.log(y)}/>