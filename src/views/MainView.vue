<script setup lang="ts">
import "../assets/styles/windows.css";
import ProfileCard from "@/components/ProfileCard.vue";
import TechAndSocialsCard from "@/components/TechAndSocialsCard.vue";
import InfoCard from "@/components/InfoCard.vue";

// Sadly I have to mess up the code and import the images
// ... *sigh*
import aboutIcon from "@/assets/svg/heart.svg";
import projectsIcon from "@/assets/svg/article.svg";
import workstationIcon from "@/assets/svg/computer.svg";
import downasaurIcon from "@/assets/svg/downasaur.svg";
</script>

<template>
  <main class="flex col g-xxl">
    <ProfileCard />

    <div class="information grid g-x">
      <InfoCard 
        title="About" 
        to="/about" 
        :icon-url="aboutIcon" 
        class="info-card"
        style="animation-delay: 0.1s"
      />
      <InfoCard 
        title="Projects" 
        to="/projects" 
        :icon-url="projectsIcon" 
        class="info-card"
        style="animation-delay: 0.2s"
      />
      <InfoCard 
        title="Experience" 
        to="/experience" 
        :icon-url="workstationIcon" 
        class="info-card"
        style="animation-delay: 0.3s"
      />
      <InfoCard 
        title="Hobbies" 
        to="/hobbies" 
        :icon-url="downasaurIcon" 
        class="info-card"
        style="animation-delay: 0.4s"
      />
    </div>
    <TechAndSocialsCard />
  </main>
</template>

<style scoped>
/* Existing Styles */
.information {
  grid-template-columns: 1fr 1fr 1fr 1fr;
}

.info-card {
  opacity: 0;
  transform: translateY(30px) scale(0.95);
  animation: slideInUp 0.6s ease-out forwards;
  transition: all 0.3s cubic-bezier(0.34, 1.56, 0.64, 1);
  position: relative;
}

.info-card:hover {
  transform: translateY(-8px) scale(1.05);
  filter: brightness(1.1);
  box-shadow: 0 15px 35px rgba(134, 193, 252, 0.2);
}

.info-card:hover::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(45deg, rgba(134, 193, 252, 0.1), rgba(204, 204, 128, 0.1));
  border-radius: inherit;
  z-index: -1;
  animation: pulseGlow 0.6s ease-out;
}

.info-card:active {
  transform: translateY(-4px) scale(1.02);
  transition: all 0.1s ease;
}

@keyframes slideInUp {
  0% {
    opacity: 0;
    transform: translateY(30px) scale(0.95);
  }
  100% {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
}

@keyframes pulseGlow {
  0% {
    opacity: 0;
    transform: scale(0.8);
  }
  50% {
    opacity: 1;
    transform: scale(1.1);
  }
  100% {
    opacity: 0.3;
    transform: scale(1);
  }
}

/** RESPONSIVE */
@media screen and (max-width: 1024px) {
  .information {
    grid-template-columns: 1fr 1fr;
  }
}
</style>