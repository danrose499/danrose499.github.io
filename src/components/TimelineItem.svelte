<script>
  import { onMount } from "svelte";
  import gsap from "gsap";

  export let side = "left";  // alternate sides: left/right
  export let title;
  export let description;
  export let image;

  let itemEl;
  let hasAnimated = false;

  onMount(() => {
    console.log('TimelineItem mounted for:', title);
    
    if (itemEl) {
      console.log('Element found:', itemEl);
      
      // Set initial state - invisible and off-screen
      gsap.set(itemEl, {
        x: side === "left" ? -300 : 300,
        opacity: 0,
        scale: 0.5,
        rotation: side === "left" ? -15 : 15
      });
      
      // Wait a bit for the page to settle, then create observer
      setTimeout(() => {
        const observer = new IntersectionObserver(
          (entries) => {
            entries.forEach((entry) => {
              if (entry.isIntersecting && !hasAnimated) {
                console.log('DRAMATIC Animation triggered for:', title);
                hasAnimated = true;
                
                gsap.to(itemEl, {
                  x: 0,
                  opacity: 1,
                  scale: 1,
                  rotation: 0,
                  duration: 1.5,
                  ease: "elastic.out(1, 0.3)",
                  onComplete: () => console.log('DRAMATIC Animation completed for:', title)
                });
              }
            });
          },
          {
            threshold: 0.3,
            rootMargin: "0px 0px -20% 0px"
          }
        );
        
        observer.observe(itemEl);
      }, 500); // Wait 500ms for page to settle
    } else {
      console.error('Element not found!');
    }
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
