<script>
  import { onMount, onDestroy } from "svelte";
  export let title = "";
  export let image = ""; // imported image path
  export let description = "";
  export let href = "#";

  let isTouch = false;
  let revealed = false;
  let el; // root anchor element

  onMount(() => {
    // Detect primary touch devices (no hover, coarse pointer)
    if (typeof window !== "undefined" && typeof window.matchMedia === "function") {
      const mq = window.matchMedia("(hover: none) and (pointer: coarse)");
      isTouch = mq.matches;
      // keep in sync if device orientation/profile changes
      const handler = (e) => (isTouch = e.matches);
      mq.addEventListener?.("change", handler);

      // Close overlay when tapping outside on touch devices
      const handleDocPointerDown = (e) => {
        if (!isTouch) return;
        if (!revealed) return;
        if (!el) return;
        if (!el.contains(e.target)) {
          revealed = false;
        }
      };
      document.addEventListener("pointerdown", handleDocPointerDown, true);

      onDestroy(() => {
        mq.removeEventListener?.("change", handler);
        document.removeEventListener("pointerdown", handleDocPointerDown, true);
      });
    }
  });

  function handleClick(event) {
    // On touch devices: first tap reveals overlay, second tap follows link
    if (isTouch && !revealed) {
      revealed = true;
      event.preventDefault();
    }
  }
</script>

<a bind:this={el} class="card" class:revealed={revealed} href={href} target="_blank" rel="noopener noreferrer" aria-label={`Open project ${title} in a new tab`} on:click={handleClick}>
  <div class="media">
    <img src={image} alt={title} loading="lazy" />
    <div class="overlay">
      <h3>{title}</h3>
      <p>{description}</p>
    </div>
  </div>
</a>

<style>
  .card {
    display: block;
    color: inherit;
    text-decoration: none;
    border-radius: 12px;
    overflow: hidden;
    background: #fff;
    box-shadow: 0 2px 8px rgba(0,0,0,0.06);
    transition: transform 0.15s ease, box-shadow 0.15s ease;
  }
  .card:focus-visible {
    outline: 3px solid #111;
    outline-offset: 2px;
  }
  .card:hover {
    transform: translateY(-2px);
    box-shadow: 0 6px 20px rgba(0,0,0,0.12);
  }

  .media {
    position: relative;
    aspect-ratio: 16 / 9;
    background: #f0f0f0;
  }
  .media img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    display: block;
    transition: filter 0.2s ease;
  }

  .overlay {
    position: absolute;
    inset: 0;
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
    gap: 0.25rem;
    padding: 1rem;
    background: linear-gradient(to top, rgba(0,0,0,0.7), rgba(0,0,0,0.25) 55%, rgba(0,0,0,0));
    color: #fff;
    opacity: 0;
    transition: opacity 0.2s ease;
  }
  .card:hover .overlay {
    opacity: 1;
  }
  .card.revealed .overlay {
    opacity: 1;
  }
  .card:hover .media img,
  .card.revealed .media img {
    filter: brightness(0.7) saturate(0.95);
  }
  .overlay h3 {
    margin: 0;
    font-size: 1.1rem;
    line-height: 1.2;
  }
  .overlay p {
    margin: 0;
    font-size: 0.9rem;
    color: #eaeaea;
  }
</style>
