<script>
  import Timeline from "./components/Timeline.svelte";
  import Projects from "./components/Projects.svelte";
  import { onMount } from "svelte";
  import linkedInImg from "./assets/images/icons/LinkedIn.png";
  import githubImg from "./assets/images/icons/GitHub.png";

  let route = "experiences";
  let animate = false;
  const HASH_PREFIX = "#/";

  function setRouteFromHash() {
    const hash = window.location.hash || "";
    const val = hash.startsWith(HASH_PREFIX) ? hash.slice(HASH_PREFIX.length) : "experiences";
    route = (val === "projects" || val === "experiences") ? val : "experiences";
  }

  onMount(() => {
    const start = () => {
      animate = true;
      const t = setTimeout(() => {
        animate = false;
      }, 3000);
      return t;
    };
    let timeoutId;
    if (typeof requestAnimationFrame === "function") {
      requestAnimationFrame(() => {
        timeoutId = start();
      });
    } else {
      timeoutId = start();
    }
    // initialize route from hash
    setRouteFromHash();

    return () => {
      clearTimeout(timeoutId);
    };
  });
</script>

<svelte:window on:hashchange={setRouteFromHash} />

<header class="toolbar">
  <nav class="nav-left">
    <a class="icon" href="/" aria-label="Home">
      <img src="/assets/head.png" alt="Head" width="22" height="22">
    </a>
    <button class="nav-btn" aria-current={route === 'experiences'} on:click={() => (window.location.hash = '#/experiences')}>Experiences</button>
    <button class="nav-btn" aria-current={route === 'projects'} on:click={() => (window.location.hash = '#/projects')}>Projects</button>
  </nav>
  <div class="nav-right">
    <a class="icon" href="https://www.linkedin.com/in/rosenthal-d/" target="_blank" rel="noopener noreferrer" aria-label="LinkedIn">
      <img src={linkedInImg} alt="LinkedIn" width="22" height="22">
    </a>
    <a class="icon" href="https://github.com/danrose499" target="_blank" rel="noopener noreferrer" aria-label="GitHub">
      <img src={githubImg} alt="GitHub" width="22" height="22">
    </a>
  </div>
  
</header>

<main>
  {#if route === 'experiences'}
    <h1>👋 Hi! My name is <span class="name" class:animate={animate}>Daniel Rosenthal</span></h1>
    <h3>I'm a Software Engineer based out of NYC<br>Scroll down to see my journey</h3>
    <Timeline />
  {:else if route === 'projects'}
    <Projects />
  {/if}
</main>

<style>
main {
  font-family: sans-serif;
  background: #f5f5f5;
  min-height: 100vh;
  overflow-x: hidden;
  padding-top: 64px;
}
h1 {
  text-align: center;
  padding-top: 2rem;
  padding-left: 2rem;
  padding-right: 2rem;
}
h3 {
  text-align: center;
}

/* toolbar */
.toolbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  height: 64px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 1rem;
  background: #ffffffee;
  backdrop-filter: saturate(180%) blur(10px);
  border-bottom: 1px solid #eaeaea;
  z-index: 1000;
}
.nav-left {
  display: flex;
  gap: 0.5rem;
}
.nav-btn {
  appearance: none;
  border: 0;
  background: transparent;
  padding: 0.5rem 0.75rem;
  border-radius: 8px;
  font-weight: 600;
  color: #333;
  cursor: pointer;
}
.nav-btn:hover {
  background: #f5f5f5;
}
.nav-btn[aria-current="true"] {
  background: #111;
  color: #fff;
}
.nav-btn:focus-visible {
  outline: 2px solid #111;
  outline-offset: 2px;
}
.nav-right {
  display: flex;
  align-items: center;
  gap: 0.75rem;
}
.icon {
  color: #333;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 36px;
  height: 36px;
  border-radius: 50%;
}
.icon:hover {
  background: #f0f0f0;
}

.name {
  display: inline-block;
  transition: all 0.3s ease;
  cursor: default;
  color: #111;
  -webkit-text-fill-color: currentColor;
}

.name.animate {
  background: linear-gradient(45deg, #ff0000, #ff7f00, #ffff00, #00ff00, #0000ff, #4b0082, #9400d3);
  background-size: 300% 300%;
  background-clip: text;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  animation: rainbow 2s ease-in-out 2 both, endfade 0.3s ease 3.9s forwards;
  will-change: background-position;
}

.name:hover {
  background: linear-gradient(45deg, #ff0000, #ff7f00, #ffff00, #00ff00, #0000ff, #4b0082, #9400d3);
  background-size: 300% 300%;
  background-clip: text;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  animation: rainbow 2s ease-in-out infinite;
  transform: scale(1.05);
}

@keyframes rainbow {
  0% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}

@keyframes endfade {
  from {
    opacity: 1;
  }
  to {
    opacity: 0.9;
  }
}

@media (max-width: 640px) and (orientation: portrait) {
  h1,
  h3 {
    padding-left: 1rem;
    padding-right: 1rem;
  }
}
</style>
