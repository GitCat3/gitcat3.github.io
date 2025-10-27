<script>
  import { Canvas } from '@threlte/core';
  import Scene from './Scene.svelte';
  import { onMount } from 'svelte';
  import ChevronsDown from 'lucide-svelte/icons/chevrons-down';
  import { fade } from 'svelte/transition';

  let displayText = "";
  let index = 0;
  let isDeleting = false;
  let charIndex = 0;
  const texts = ["Websites", "Minecraft Mods", "Desktop Apps", "Other Random Coding Projects"];
  let chevronOpacity = 1;

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

  function handleScroll() {
    const scrollPosition = window.scrollY;
    const fadeStart = 0;
    const fadeEnd = 300;
    
    if (scrollPosition <= fadeStart) {
      chevronOpacity = 1;
    } else if (scrollPosition >= fadeEnd) {
      chevronOpacity = 0;
    } else {
      chevronOpacity = 1 - (scrollPosition - fadeStart) / (fadeEnd - fadeStart);
    }
  }

  onMount(() => {
    typeEffect();
    
    // Add scroll event listener
    window.addEventListener('scroll', handleScroll);
    
    // Initialize GitHub embed after DOM is ready
    // @ts-ignore
    github_embed_repo.default('repo-details', 'GitCat3', 'Rust-Trig-Calculator', {
      showProfile: true,
      showStats: true,
      theme: 'dark',
      statsToShow: ['stars', 'forks', 'watchers', 'issues', 'pull_requests', 'contributors'],
      component: 'card'
    });

    // @ts-ignore
    github_embed_repo.default('repo-details2', 'GitCat3', 'picalc', {
      showProfile: true,
      showStats: true,
      theme: 'dark',
      statsToShow: ['stars', 'forks', 'watchers', 'issues', 'pull_requests', 'contributors'],
      component: 'card'
    });

    // @ts-ignore
    github_embed_repo.default('repo-details3', 'GitCat3', 'Marlin', {
      showProfile: true,
      showStats: true,
      theme: 'dark',
      statsToShow: ['stars', 'forks', 'watchers', 'issues', 'pull_requests', 'contributors'],
      component: 'card'
    });

    // Cleanup scroll listener
    return () => {
      window.removeEventListener('scroll', handleScroll);
    };
  });
</script>

<head>
  <link href="https://fonts.googleapis.com/css2?family=Lato:ital,wght@0,100;0,300;0,400;0,700;0,900;1,100;1,300;1,400;1,700;1,900&display=swap" rel="stylesheet">
  <script src="https://cdn.jsdelivr.net/npm/github-embed-repo/dist/github_embed_repo.min.js"></script>
  <title>GitCat3</title>
</head>

<body style="background-color: rgb(11, 16, 28);">
  <section>
    <div id="canvas">
      <Canvas>
        <Scene />
      </Canvas>
    </div>
    <div id="canvas-overlay1">
      <p id="welcometext">
        I Make {displayText}
      </p>
    </div>
    <div id="canvas-overlay-github-button">
      <a href="https://github.com/GitCat3/" target="_blank" rel="noopener noreferrer">
        <img src="github.png" alt="GitCat3's Github page" width=64 height=64 style="transition: transform 0.3s ease;" />
      </a>
    </div>
    <div id="canvas-overlay-chevrons-down" style="opacity: {chevronOpacity}; transition: opacity 0.1s ease-out;">
      <ChevronsDown size=90px color="#a60000" />
    </div>
  </section>
  
  <div style="text-align: center; background: transparent; color: grey; margin: 50px auto; max-width: 900px; padding: 0 20px; position: relative; font-size: 18px; line-height: 1.6;" >
    <p>
      Hello there! I am GitCat3, a software hobbyist with a passion for creating a multitude of things, including
      websites, Minecraft mods, desktop apps, and more! I got my start with Python, and quickly branched out into C,
      which enabled me to learn a multitude of other programming languages, such as Java and C#, much faster. Recently,
      I have been diving into Rust, and two of the projects that are showcased below are built usint Rust. Additionally,
      I am a maker outside of just programming; I also enjoy 3D printing and electronics. I have an Ender 5 Pro, and the other
      repo showcased below is my custom Marlin firmware to use the Ender 5 Pro with a BLTouch sensor, as well as other mods I
      have done for it. Feel free to explore my projects below, or press the little GitHub icon in the corner of this page to
      explore my full GitHub profile!
    </p>
  </div>

  <div style="display: flex; gap: 20px; justify-content: center; margin: 50px auto; max-width: 1100px; flex-wrap: wrap; align-items: stretch;">
    <div id="repo-details" style="flex: 1 1 350px; max-width: 400px;"></div>
    <div id="repo-details2" style="flex: 1 1 350px; max-width: 400px;"></div>
    <div id="repo-details3" style="flex: 1 1 350px; max-width: 400px;"></div>
  </div>
</body>

<style lang="scss">
  section {
    position: relative;
    width: 100%;
    height: 100vh;

    #canvas-overlay1 {
      position: absolute;
      top: 10%;
      left: 50%;
      transform: translate(-50%, -50%);
    }

    #canvas-overlay-github-button {
      position: fixed;
      top: 95%;
      left: 95%;
      transform: translate(-50%, -50%);
      
      img:hover {
        transform: scale(1.2);
      }
    }

    #canvas-overlay-chevrons-down {
      position: absolute;
      top: 95%;
      left: 50%;
      transform: translate(-50%, -50%);
    }

    #canvas {
      width: 100%;
      height: 100%;
      display: block;
      position: fixed;
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
    content: "";
    position: absolute;
    top: 10%;
    bottom: 10%;
    right: 0;
    width: 2px;
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

  body {
    margin: 0;
    overflow-x: hidden;
  }
</style>
