<script>
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
      title="Software Engineer"
      company="BNY Mellon - Pershing"
      dateRange="2023 - Present"
      description={[
        "Develop and maintain trading platform systems",
        "Implement scalable microservices architecture",
        "Collaborate with cross-functional teams on system integration"
      ]}
      image={pershingImg}
      companyUrl="https://www.bnymellon.com"
    />
    <TimelineItem
      side="right"
      title="Software Engineer"
      company="BNY Mellon"
      dateRange="2022 - 2023"
      description="Developed financial applications and services using modern web technologies. Focused on backend systems and API development."
      image={bnyImg}
      companyUrl="https://www.bnymellon.com"
    />
    <TimelineItem
      side="left"
      title="Student"
      company="City College of New York (CCNY)"
      dateRange="2018 - 2022"
      description="B.S. in Computer Science with focus on software engineering and data structures. Relevant coursework included algorithms, databases, and software development."
      image={ccnyImg}
      companyUrl="https://www.ccny.cuny.edu"
    />
    <TimelineItem
      side="right"
      title="Graduate"
      company="Dr. Ronald E. McNair High School"
      dateRange="2014 - 2018"
      description="High school diploma with honors. Participated in robotics club and computer science competitions."
      image={drsImg}
      companyUrl="https://www.schools.nyc.gov"
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