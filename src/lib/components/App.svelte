<script>
  import { Canvas } from '@threlte/core';
  import Scene from './Scene.svelte';
  import { onMount } from 'svelte';

  let displayText = "";
  let index = 0;
  let isDeleting = false;
  let charIndex = 0;
  const texts = ["Website", "Minecraft Mod", "Desktop Application", "Other Random Coding Project"];

  function typeEffect() {
    const currentText = texts[index];
    const speed = isDeleting ? 100 : 200;
    if (isDeleting) {
      displayText = currentText.substring(0, charIndex--);
    } else {
      displayText = currentText.substring(0, charIndex++);
    }
    if (!isDeleting && charIndex === currentText.length) {
      setTimeout(() => (isDeleting = true), 1500);
    } else if (isDeleting && charIndex === 0) {
      isDeleting = false;
      index = (index + 1) % texts.length;
    }
    setTimeout(typeEffect, speed);
  }

  onMount(typeEffect);
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
  <div id="canvas-overlay1">
    <p id="welcometext">
      Welcome To Your Next {displayText}
    </p>
  </div>
  <div id="canvas-overlay2">
    <a href="https://github.com/GitCat3/" target="_blank" rel="noopener noreferrer">
      <img src="github.png" alt="GitCat3's Github page" width=64 height=64 style="transition: transform 0.3s ease;" />
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

  #welcometext {
    color: white;
    font-size: 40px;
    font-family: 'Lato', serif;
    white-space: nowrap;
    position: relative;
  }

  #welcometext::after {
    content: ""; /* Create the cursor */
    position: absolute;
    top: 0;
    right: 0;
    width: 2px;
    height: 1em;
    background-color: white;
    animation: blink 0.7s step-end infinite;
  }

  @keyframes blink {
    0%, 100% {
      opacity: 1;
    }
    50% {
      opacity: 0;
    }
  }
</style>
