<script>
  import { Canvas } from '@threlte/core';
  import Scene from './Scene.svelte';
  import { onMount } from 'svelte';
  import ChevronsDown from 'lucide-svelte/icons/chevrons-down';

  let displayText = "";
  let index = 0;
  let isDeleting = false;
  let charIndex = 0;
  const texts = ["Websites", "Minecraft Mods", "Desktop Apps", "Other Random Coding Projects"];

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

  onMount(() => {
    typeEffect();
    
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
    github_embed_repo.default('repo-details2', 'GitCat3', 'Rust-Trig-Calculator', {
      showProfile: true,
      showStats: true,
      theme: 'dark',
      statsToShow: ['stars', 'forks', 'watchers', 'issues', 'pull_requests', 'contributors'],
      component: 'card'
    });

    // @ts-ignore
    github_embed_repo.default('repo-details3', 'GitCat3', 'Rust-Trig-Calculator', {
      showProfile: true,
      showStats: true,
      theme: 'dark',
      statsToShow: ['stars', 'forks', 'watchers', 'issues', 'pull_requests', 'contributors'],
      component: 'card'
    });
  });
</script>

<head>
  <link href="https://fonts.googleapis.com/css2?family=Lato:ital,wght@0,100;0,300;0,400;0,700;0,900;1,100;1,300;1,400;1,700;1,900&display=swap" rel="stylesheet">
  <script src="https://cdn.jsdelivr.net/npm/github-embed-repo/dist/github_embed_repo.min.js"></script>
  <title>GitCat3's Awesome Website</title>
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
    <div id="canvas-overlay-chevrons-down">
      <ChevronsDown size=90px color="#a60000"/>
    </div>
  </section>
  
  <div style="text-align: center; background: transparent; color: grey; margin: 50px auto; max-width: 900px; padding: 0 20px; position: relative; font-size: 18px; line-height: 1.6;" >
    <p>
      Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. 
      Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. 
      Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. 
      Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
    </p>
  </div>

  <div style="display: flex; gap: 20px; justify-content: center; margin: 50px auto; max-width: 1200px; flex-wrap: wrap;">
    <div id="repo-details"></div>
    <div id="repo-details2"></div>
    <div id="repo-details3"></div>
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

  body {
    margin: 0;
    overflow-x: hidden;
  }
</style>
