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
      title="Software Engineer (Senior Associate)"
      company="BNY Pershing"
      dateRange="August 2022 - Present"
      description={[
        "Designed and led development of a high-performance Java Spring Boot backend that processes 100K-200K SWIFT messages daily from IBM MQ, optimizing message parsing efficiency.",
        "Developed a Java/Angular real-time trading dashboard that consumes 2M-2.5M Kafka messages daily, enabling seamless trade monitoring and improving operational visibility.",
        "Created an internal VS Code extension for SWIFT message formatting and tag tooltips, reducing manual effort for developers.",
        "Automated Splunk data extraction using Python and shell scripts to analyze user trends, improving system monitoring and decision-making.",
        "Led technical interviews for hiring initiatives and revamped HackerRank problem sets for BNY’s early career program.",
        "Refactored legacy applications, reducing SonarQube-reported technical debt by over 4 days and improving maintainability.",
        "Mentored new graduates and interns through the BNY Early Campus Mentorship program, fostering technical growth and onboarding efficiency."
      ]}
      image={pershingImg}
      companyUrl="https://www.bny.com/pershing"
    />
    <TimelineItem
      side="right"
      title="Software Engineer (Intern)"
      company="BNY"
      dateRange="June 2021 - August 2021"
      description={[
        "Enhanced unit test coverage of legacy production code using JUnit and Mockito, increasing code quality and reducing bug occurrences.",
        "Developed reusable, parameterized testing classes to eliminate thousands of lines of redundant code, streamlining testing efficiency."
      ]}
      image={bnyImg}
      companyUrl="https://www.bny.com"
    />
    <TimelineItem
      side="left"
      title="Student"
      company="City College of New York (CCNY)"
      dateRange="2018 - 2022"
      description={[
        "B.S. in Computer Science with focus on software engineering and data structures. Relevant coursework included algorithms, databases, and software development."
      ]}
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

@media (max-width: 640px) and (orientation: portrait) {
  .timeline-container {
    width: 100%;
    padding: 2rem 1rem;
    box-sizing: border-box;
  }

  .timeline {
    gap: 1.25rem;
    align-items: stretch;
  }
}
</style>