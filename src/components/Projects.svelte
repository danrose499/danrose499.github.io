<script>
  import ProjectCard from "./ProjectCard.svelte";
  import musicMateImg from "../assets/images/projects/MusicMate.png";
  import danBotImg from "../assets/images/projects/DanBot.png";
  import pocketEarthImg from "../assets/images/projects/pocketEarth.png";

  const projects = [
    {
      title: "Music Mate",
      image: musicMateImg,
      description: "A Svelte app to explore keys and build/play simple chord progressions with guitar and ukulele diagrams",
      href: "https://danielrosenthal.dev/Music-Mate/"
    },
    {
      title: "DanBot",
      image: danBotImg,
      description: "My very own chatbot that you can use to learn more about me and what I'm up to!",
      href: "https://danielrosenthal.dev/danBot/"
    },
    {
      title: "Pocket Earth",
      image: pocketEarthImg,
      description: "Work in Progress... Explore earth, from your pocket!",
      href: "https://danielrosenthal.dev/pocket-earth/"
    },
  ];
</script>

<section class="projects">
  <h1>These are some projects that I've worked on</h1>
  <div class="grid">
    {#each projects as p}
      <ProjectCard title={p.title} image={p.image} description={p.description} href={p.href} />
    {/each}
  </div>
  <div class="note" aria-hidden={true}>
    Click on a project to open it in a new tab.
  </div>
  
</section>

<style>
  .projects {
    min-height: calc(100vh - 64px);
    background: #f5f5f5;
    padding: 2rem 1rem 3rem;
    max-width: 1100px;
    margin: 0 auto;
  }
  h1 {
    text-align: center;
    margin: 0 0 1.25rem 0;
  }
  .grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
    gap: 1rem;
    align-items: stretch;
  }
  .note {
    text-align: center;
    color: #666;
    font-size: 0.95rem;
    margin-top: 1rem;
  }
  @media (min-width: 640px) {
    .projects {
      padding: 2.5rem 1.5rem 3.5rem;
    }
    .grid {
      gap: 1.25rem;
    }
  }
</style>
