<script>
  import { T } from '@threlte/core'
  import { ContactShadows, Float, Grid, ImageMaterial, HTML} from '@threlte/extras'
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

<Float floatIntensity={0.5} floatingRange={[0,1]}>
  <T.Mesh position={[0, 1, 0]}>
    <T.BoxGeometry />
    <ImageMaterial url="/rainbowcat.jpg"/>
  </T.Mesh>
</Float>
