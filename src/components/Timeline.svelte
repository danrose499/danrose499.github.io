<script>
  import { onMount } from "svelte";
  import gsap from "gsap";
  import { ScrollTrigger } from "gsap/ScrollTrigger";
  import TimelineItem from "./TimelineItem.svelte";

  import ccnyImg from "../assets/images/CCNY.png";
  import bnyImg from "../assets/images/BNY.png";
  import pershingImg from "../assets/images/BNY_Pershing.svg";
  import drsImg from "../assets/images/DRS.png";
</script>

<div class="timeline-container">
  <div class="timeline">
    <TimelineItem
    side="left"
    title="Current Position"
    description={[
        "Software Engineer at XYZ",
        "Working on frontend and backend",
        "Leading a small team"
    ]}
    image={pershingImg}
    />
    <TimelineItem
      side="right"
      title="Current Position"
      description="Software Engineer at XYZ"
      image={bnyImg}
    />
    <TimelineItem
      side="left"
      title="College"
      description="B.S. Computer Science at ABC University"
      image={ccnyImg}
    />
    <TimelineItem
      side="right"
      title="High School"
      description="Graduated in 2015"
      image={drsImg}
    />
  </div>
</div>

<style>
.timeline-container {
  width: 80%;
  margin: 0 auto;
  padding: 4rem 0;
}

.timeline {
  display: flex;
  flex-direction: column;
  align-items: center; /* Center items horizontally */
  gap: 2rem; /* Space between items */
}

/* Removed .timeline-line styles */
</style>