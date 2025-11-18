<script>
  import { onMount } from 'svelte';
  
  onMount(() => {
    // Update the URL to show 404 in the path
    if (window.location.hash !== '#/404') {
      window.history.replaceState({}, '', '#/404');
    }
  });
</script>

<div class="not-found">
  <h1>404 - Page Not Found</h1>
  <p>Oops! The page you're looking for doesn't exist or has been moved.</p>
  <a href="#/experiences" class="back-link">← Back to Home</a>
</div>

<style>
  .not-found {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 70vh;
    text-align: center;
    padding: 0 1rem;
  }
  
  h1 {
    font-size: 2.5rem;
    margin-bottom: 1rem;
    color: var(--text-color);
  }
  
  p {
    font-size: 1.2rem;
    margin-bottom: 2rem;
    color: var(--text-secondary);
  }
  
  .back-link {
    display: inline-block;
    padding: 0.75rem 1.5rem;
    background-color: var(--primary-color);
    color: white;
    text-decoration: none;
    border-radius: 4px;
    transition: background-color 0.2s ease;
  }
  
  .back-link:hover {
    background-color: var(--primary-hover);
  }
</style>
