<script>
  import { onMount } from "svelte";
  import gsap from "gsap";

  export let side = "left";  // alternate sides: left/right
  export let title;
  export let description;
  export let image;
  export let company; // new prop for company/project name
  export let dateRange; // new prop for date range
  export let companyUrl; // new prop for company website URL

  let itemEl;
  let hasAnimated = false;

  function handleImageClick() {
    if (companyUrl) {
      window.open(companyUrl, '_blank', 'noopener,noreferrer');
    }
  }

  onMount(() => {
    console.log('TimelineItem mounted for:', title);
    
    if (itemEl) {
      console.log('Element found:', itemEl);
      
      // Set initial state - slightly off-screen and invisible
      gsap.set(itemEl, {
        x: side === "left" ? -50 : 50,
        opacity: 0
      });
      
      // Wait a bit for the page to settle, then create observer
      setTimeout(() => {
        const observer = new IntersectionObserver(
          (entries) => {
            entries.forEach((entry) => {
              if (entry.isIntersecting && !hasAnimated) {
                // Moderate slide and fade in
                console.log('Slide in animation triggered for:', title);
                hasAnimated = true;
                
                gsap.to(itemEl, {
                  x: 0,
                  opacity: 1,
                  duration: 1,
                  ease: "power2.out"
                });
              } else if (!entry.isIntersecting && hasAnimated) {
                // Moderate slide and fade out when scrolling back up
                console.log('Slide out animation triggered for:', title);
                hasAnimated = false;
                
                gsap.to(itemEl, {
                  x: side === "left" ? -50 : 50,
                  opacity: 0,
                  duration: 0.7,
                  ease: "power2.in"
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
    {#if company}
      <div 
        class="company {companyUrl ? 'clickable' : ''}"
        on:click={handleImageClick}
        role={companyUrl ? 'button' : 'div'}
        tabindex={companyUrl ? '0' : null}
        on:keydown={(e) => companyUrl && e.key === 'Enter' && handleImageClick()}
      >
        {company}
      </div>
    {/if}
    {#if dateRange}
      <div class="date-range">{dateRange}</div>
    {/if}
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
    <img 
      src={image} 
      alt={company || title} 
      class="graphic {companyUrl ? 'clickable' : ''}"
      on:click={handleImageClick}
      role={companyUrl ? 'button' : 'img'}
      tabindex={companyUrl ? '0' : null}
      on:keydown={(e) => companyUrl && e.key === 'Enter' && handleImageClick()}
    />
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

.company {
  font-size: 1.1rem;
  font-weight: 600;
  color: #2c3e50;
  margin-top: 0.2rem;
  margin-bottom: 0.3rem;
}

.company.clickable {
  cursor: pointer;
  transition: color 0.2s ease;
}

.company.clickable:hover {
  color: #3498db;
}

.company.clickable:focus {
  outline: 2px solid #3498db;
  outline-offset: 2px;
  border-radius: 4px;
}

.date-range {
  font-size: 0.9rem;
  color: #7f8c8d;
  font-style: italic;
  margin-bottom: 0.5rem;
}

.graphic {
  width: 120px;
  height: auto;
  margin: 0 1rem;
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.graphic.clickable {
  cursor: pointer;
  border-radius: 8px;
  padding: 4px;
}

.graphic.clickable:hover {
  transform: scale(1.05);
  box-shadow: 0 4px 15px rgba(0,0,0,0.2);
}

.graphic.clickable:focus {
  outline: 2px solid #3498db;
  outline-offset: 2px;
}

.content ul {
  margin: 0.5rem 0 0 1.2rem;
  padding: 0;
}
.content li {
  margin-bottom: 0.3rem;
}
</style>
