<script>
  import { onMount } from "svelte";
  import gsap from "gsap";
  import { ScrollTrigger } from "gsap/ScrollTrigger";

  export let side = "left";  // alternate sides: left/right
  export let title;
  export let description;
  export let image;

  let itemEl;

  onMount(() => {
    gsap.registerPlugin(ScrollTrigger);

    gsap.from(itemEl, {
      x: side === "left" ? -200 : 200,
      opacity: 0,
      duration: 1,
      scrollTrigger: {
        trigger: itemEl,
        start: "top 80%", // when 80% of viewport hits item
        toggleActions: "play none none reverse"
      }
    });
  });
</script>

<div class="timeline-item {side}" bind:this={itemEl}>
  <div class="content">
    <h3>{title}</h3>
    {#if Array.isArray(description)}
      <ul>
        {#each description as point}
          <li>{point}</li>
        {/each}
      </ul>
    {:else}
      <p>{description}</p>
    {/if}
  </div>
  {#if image}
    <img src={image} alt={title} class="graphic" />
  {/if}
</div>

<style>
.timeline-item {
  display: flex;
  align-items: center;
  margin: 4rem 0;
}
.timeline-item.left { flex-direction: row; }
.timeline-item.right { flex-direction: row-reverse; }

.content {
  max-width: 300px;
  background: white;
  padding: 1rem;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
}
.graphic {
  width: 120px;
  height: auto;
  margin: 0 1rem;
}
.timeline-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin: 4rem 0;
  position: relative;
  z-index: 2;
}
.timeline-item.left { flex-direction: row; }
.timeline-item.right { flex-direction: row-reverse; }

.content {
  max-width: 300px;
  background: white;
  padding: 1rem;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
}

.graphic {
  width: 120px;
  height: auto;
  margin: 0 1rem;
}

.content ul {
  margin: 0.5rem 0 0 1.2rem;
  padding: 0;
}
.content li {
  margin-bottom: 0.3rem;
}
</style>
