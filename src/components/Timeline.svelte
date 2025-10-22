<script>
  import TimelineItem from "./TimelineItem.svelte";

  import ccnyImg from "../assets/images/CCNY.png";
  import bnyImg from "../assets/images/BNY.png";
  import pershingImg from "../assets/images/BNY_Pershing.png";
  import cunyImg from "../assets/images/CUNY.png";
  import nySenateImg from "../assets/images/NY_Senate.png";
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
      title="Computer Science Tutor"
      company="CUNY 2X Tech"
      dateRange="January 2020 - May 2020"
      description={[
        "Conducted biweekly tutoring sessions to support struggling computer science students at The City College of New York (CUNY).",
        "Adapted teaching strategies to remote learning during COVID-19, ensuring continued academic support.",
        "Contributed to the CUNY 2X Tech initiative, helping increase the number of CUNY graduates in tech-related fields."
      ]}
      image={cunyImg}
      companyUrl="https://www.ccny.cuny.edu/news/city-college-partners-nyc-increase-number-tech-grads"
    />
    <TimelineItem
      side="right"
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
      side="left"
      title="Summer Intern"
      company="New York State Senate"
      dateRange="July 2016 - August 2016"
      description={[
        "Summer Intern for New York State Senator Todd Kaminsky (9th District)",
        "Spoke with constituents over the phone and in person to help the Senator better evaluate the needs of his district",
        "Managed casework to allow the office to run as efficiently as possible"
      ]}
      image={nySenateImg}
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