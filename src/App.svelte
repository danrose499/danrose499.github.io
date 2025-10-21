<script>
  import Timeline from "./components/Timeline.svelte";
</script>

<main>
  <h1>👋 Hi! My name is <span class="name">Daniel Rosenthal</span></h1>
  <h3>I'm a Software Enginner based out of NYC<br>Scroll down to see my journey</h3>
  <Timeline />
</main>

<style>
main {
  font-family: sans-serif;
  background: #f5f5f5;
  min-height: 100vh;
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

.name {
  display: inline-block;
  transition: all 0.3s ease;
  cursor: default;
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
</style>
