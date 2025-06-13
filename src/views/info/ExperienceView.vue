<script setup lang="ts">
import { ref } from "vue";

const experiences = ref([
  {
    company: "Colt India",
    location: "Gurugram, Haryana",
    position: "Digital Strategy & Architecture Intern",
    duration: "June 2025 – Present",
    logo: "https://logo.clearbit.com/colt.net",
    description: "Building enterprise systems that actually scale 🏗️",
    achievements: "Engineered architectural components supporting 10,000+ users while mastering TOGAF Zachman framework. Authored 5+ design documents for UK clients and delivered technical analysis for cloud migration proposals across 10+ enterprise systems.",
    technologies: ["TOGAF", "Zachman", "Enterprise Architecture", "Cloud Migration"]
  },
  {
    company: "SNUG Technologies",
    location: "Gurugram, India",
    position: "Full Stack Developer Intern",
    duration: "June 2024 – July 2024",
    logo: "https://www.snug.in/images/Logo2.png",
    description: "Making Angular apps faster than my coffee breaks ⚡",
    achievements: "Upgraded Angular app to v17 with modular architecture, implemented SSR pipeline reducing TTFB by 30%, and configured Docker containers cutting onboarding time by 50%. Boosted Lighthouse score by 25 points.",
    technologies: ["Angular 17", "TypeScript", "Docker", "SSR", "Performance"]
  },
  {
    company: "Colt India",
    location: "Gurugram, Haryana",
    position: "Operations & Testing Intern",
    duration: "December 2023 – February 2024",
    logo: "https://logo.clearbit.com/colt.net",
    description: "Professional bug hunter with a 30% success rate 🐛",
    achievements: "Specialized in test automation and CI/CD pipeline optimization. Developed Python automation scripts reducing manual testing by 30% while executing comprehensive regression testing across multiple projects.",
    technologies: ["Python", "Test Automation", "CI/CD", "Quality Assurance"]
  },
  {
    company: "Next Tech Lab",
    location: "SRM Institute",
    position: "UI/UX Designer",
    duration: "October 2023 – Present",
    logo: "https://pbs.twimg.com/profile_images/1542746125761146880/Vs9felK2_400x400.jpg",
    description: "Turning wireframes into works of art 🎨",
    achievements: "Design lead for hackathons and group projects using MERN stack. Created social media content and recruitment materials while maintaining consistent brand identity across digital platforms.",
    technologies: ["Figma", "MERN Stack", "UI/UX", "Brand Design"]
  },
  {
    company: "SRMKZILLA",
    location: "SRM Institute",
    position: "Associate Editorial Lead",
    duration: "2023 – Present",
    logo: "https://logo.clearbit.com/srmkzilla.net",
    description: "Visual storyteller for tech events 📱",
    achievements: "Designed comprehensive materials for MOZOHACK 2 & 3 including event websites, social media campaigns, and branded merchandise. Developed design systems ensuring consistency across all SRMKZILLA communications.",
    technologies: ["Figma", "Event Design", "Social Media", "Visual Identity"]
  }
]);
</script>

<template>
  <div class="experience-view">
    <div class="experience-header">
      <h1 class="experience-title">
        <span class="title-icon">💼</span>
        Work Experience
      </h1>
      <p class="subtitle">Building things, breaking things, learning things</p>
    </div>

    <div class="experience-masonry">
      <div 
        v-for="(experience, index) in experiences" 
        :key="index" 
        class="experience-card window"
        :class="{ 'card-offset': index % 2 === 1 }"
      >
        <div class="card-header">
          <div class="company-section">
            <img :src="experience.logo" :alt="experience.company" class="company-logo" />
            <div class="company-info">
              <h3 class="company-name">{{ experience.company }}</h3>
              <p class="location">{{ experience.location }}</p>
            </div>
          </div>
          <div class="duration">{{ experience.duration }}</div>
        </div>
        
        <div class="card-content">
          <h4 class="position">{{ experience.position }}</h4>
          <p class="description">{{ experience.description }}</p>
          <p class="achievements">{{ experience.achievements }}</p>
          
          <div class="tech-stack">
            <span v-for="tech in experience.technologies" :key="tech" class="tech-tag">
              {{ tech }}
            </span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.experience-view {
  padding: 2rem;
  max-width: 1400px;
  margin: 0 auto;
}

.experience-header {
  text-align: center;
  margin-bottom: 3rem;
}

.experience-title {
  font-size: clamp(2.5rem, 6vw, 3.5rem);
  color: var(--color-accent);
  margin: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 1rem;
}

.title-icon {
  font-size: clamp(2.5rem, 6vw, 3.5rem);
  animation: bounce 2s infinite;
}

.subtitle {
  font-size: clamp(1rem, 2.5vw, 1.2rem);
  color: var(--fg-light);
  opacity: 0.8;
  margin: 0.5rem 0 0 0;
  font-weight: 400;
}

.experience-masonry {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
  gap: 2rem;
  align-items: start;
}

.experience-card {
  padding: 1.5rem;
  border-radius: 12px;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  background: var(--bg-secondary);
  border: 2px solid var(--fg-light);
  position: relative;
  animation: wobble 4s ease-in-out infinite;
}

.card-offset {
  margin-top: 2rem;
  animation: wobble-offset 4s ease-in-out infinite;
}

.experience-card:hover {
  transform: translateY(-8px);
  scale: 1.1;
  box-shadow: 0 16px 40px rgba(134, 193, 252, 0.25);
  border-color: var(--color-accent);
  animation-play-state: paused;
}

.card-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: 1rem;
  flex-wrap: wrap;
  gap: 1rem;
}

.company-section {
  display: flex;
  align-items: center;
  gap: 0.8rem;
  flex: 1;
}

.company-logo {
  width: 40px;
  height: 40px;
  border-radius: 8px;
  object-fit: contain;
  object-position: contain;
  border: 2px solid rgba(134, 193, 252, 0.2);
  transition: all 0.3s ease;
}

.company-logo:hover {
  border-color: var(--color-accent);
  transform: scale(1.1);
}

.company-info {
  flex: 1;
}

.company-name {
  font-size: clamp(1.1rem, 2.5vw, 1.3rem);
  font-weight: 700;
  color: var(--color-accent);
  margin: 0;
  line-height: 1.2;
}

.location {
  font-size: clamp(0.75rem, 1.8vw, 0.85rem);
  color: var(--fg-light);
  opacity: 0.7;
  margin: 0.2rem 0 0 0;
}

.duration {
  font-size: clamp(0.75rem, 1.8vw, 0.85rem);
  color: var(--fg-light);
  opacity: 0.8;
  font-weight: 500;
  text-align: right;
  white-space: nowrap;
}

.card-content {
  border-top: 1px solid rgba(134, 193, 252, 0.15);
  padding-top: 1rem;
}

.position {
  font-size: clamp(1rem, 2.2vw, 1.2rem);
  font-weight: 600;
  color: var(--fg-light);
  margin: 0 0 0.8rem 0;
  line-height: 1.3;
}

.description {
  font-size: clamp(0.9rem, 2vw, 1rem);
  color: var(--color-accent);
  font-style: italic;
  margin: 0 0 1rem 0;
  font-weight: 500;
  line-height: 1.4;
}

.achievements {
  font-size: clamp(0.85rem, 1.9vw, 0.95rem);
  line-height: 1.6;
  color: var(--fg-light);
  margin: 0 0 1.2rem 0;
  opacity: 0.9;
}

.tech-stack {
  display: flex;
  flex-wrap: wrap;
  gap: 0.4rem;
}

.tech-tag {
  background: rgba(134, 193, 252, 0.1);
  color: var(--fg-light);
  padding: 0.25rem 0.6rem;
  border-radius: 6px;
  font-size: clamp(0.7rem, 1.6vw, 0.75rem);
  border: 1px solid rgba(134, 193, 252, 0.25);
  transition: all 0.3s ease;
  font-weight: 500;
}

.tech-tag:hover {
  background: rgba(134, 193, 252, 0.2);
  border-color: var(--color-accent);
  transform: translateY(-2px);
}



@keyframes bounce {
  0%, 20%, 50%, 80%, 100% {
    transform: translateY(0);
  }
  40% {
    transform: translateY(-10px);
  }
  60% {
    transform: translateY(-5px);
  }
}

/* Responsive Design */
@media screen and (max-width: 900px) {
  .experience-masonry {
    grid-template-columns: 1fr;
    gap: 1.5rem;
  }

  .card-offset {
    margin-top: 0;
  }
}

@media screen and (max-width: 768px) {
  .experience-view {
    padding: 1rem;
  }
  
  .experience-header {
    margin-bottom: 2rem;
  }
  
  .experience-card {
    padding: 1.2rem;
  }

  .card-header {
    flex-direction: column;
    align-items: flex-start;
    gap: 0.5rem;
  }

  .duration {
    text-align: left;
  }
}

@media screen and (max-width: 480px) {
  .experience-masonry {
    gap: 1rem;
  }

  .experience-card {
    padding: 1rem;
  }

  .company-section {
    gap: 0.6rem;
  }

  .company-logo {
    width: 35px;
    height: 35px;
  }

  .tech-stack {
    gap: 0.3rem;
  }
}
@keyframes wobble {
  0%, 100% {
    transform: translateY(0px);
  }
  25% {
    transform: translateY(-8px);
  }
  50% {
    transform: translateY(4px);
  }
  75% {
    transform: translateY(-4px);
  }
}

@keyframes wobble-offset {
  0%, 100% {
    transform: translateY(4px);
  }
  25% {
    transform: translateY(-4px);
  }
  50% {
    transform: translateY(8px);
  }
  75% {
    transform: translateY(-2px);
  }
}
</style>