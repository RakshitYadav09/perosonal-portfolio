<script setup lang="ts">
    import { ref } from 'vue';
    import "@/assets/styles/info/base.css";
    import WobblyText from "@/components/text/Wobbly.vue";

    interface Project {
        id: number;
        title: string;
        subtitle: string;
        description: string;
        shortDesc: string;
        image: string | null;
        link: string;
        type: 'live' | 'github' | 'figma' | 'behance';
        technologies: string[];
        status: string;
        category: string;
    }

    const projects = ref<Project[]>([
        {
            id: 1,
            title: "LifeStock",
            subtitle: "Real-time Collaborative Planning",
            description: "A MERN + WebSockets planner that keeps everyone typing in sync, with frontend on Vercel and backend on Render.",
            shortDesc: "Sync everyone's workflow in real-time",
            image: "/img/LifeStock.png",
            link: "https://life-stock-planner.vercel.app/",
            type: "live",
            technologies: ["React", "Node.js", "WebSockets", "MongoDB"],
            status: "",
            category: "Full Stack"
        },
        {
            id: 2,
            title: "LoanSense",
            subtitle: "AI-Powered Loan Processing",
            description: "An AI loan agent that parses docs, flags missing data, and even talks back, powered by Gemini OCR, STT/TTS, and OpenCV face auth.",
            shortDesc: "Smart loan processing with AI assistance",
            image: "/img/LoanSense.png",
            link: "https://github.com/RakshitYadav09/LoanSense",
            type: "github",
            technologies: ["Gemini OCR", "OpenCV", "Machine Learning"],
            status: "",
            category: "AI/ML"
        },
        {
            id: 3,
            title: "MyVoice",
            subtitle: "Sign Language Recognition",
            description: "Turns hand signs into text in seconds using custom ML models — inclusivity with a machine learning twist.",
            shortDesc: "Breaking communication barriers with ML",
            image: "/img/MyVoice.png",
            link: "https://github.com/RakshitYadav09/MyVoice",
            type: "github",
            technologies: ["Machine Learning", "Computer Vision", "Python"],
            status: "",
            category: "AI/ML"
        },
        {
            id: 4,
            title: "Alchemist",
            subtitle: "Automated Faculty Booking",
            description: "Faculty booking made easy with a BS4 + Selenium scraper under the hood and a MERN stack frontend to tie it all together.",
            shortDesc: "Streamlined academic scheduling system",
            image: "/img/Alchemist.png",
            link: "https://github.com/AdityaRanjanJha/Alchemist",
            type: "github",
            technologies: ["Beautiful Soup", "Selenium", "MERN Stack"],
            status: "",
            category: "Automation"
        },
        {
            id: 5,
            title: "Gulf",
            subtitle: "Urban Navigation Design",
            description: "A \"don't get lost in the city\" commute app design in Figma, packed with personas, user journeys, and UX flows that keep you moving.",
            shortDesc: "Smart city navigation reimagined",
            image: "/img/Gulf.png",
            link: "https://www.figma.com/design/1N2Ev2PNkLmihQJdR3XYny/Gulf?node-id=111-18850&t=8OL0apLdjX01OzrZ-1",
            type: "figma",
            technologies: ["Figma", "UI/UX Design", "Mobile Design"],
            status: "",
            category: "UX/UI"
        },
        {
            id: 6,
            title: "Opiniox",
            subtitle: "A Betting App Design",
            description: "A sleek betting platform mockup in Figma for web and mobile, polished enough to gamble on for a freelance client.",
            shortDesc: "Elegant gaming experience design",
            image: "/img/Opiniox.png",
            link: "https://www.figma.com/design/KAmCIUv2ftbSaMjLSV95bA/Betting-App",
            type: "figma",
            technologies: ["Figma", "Web Design", "Mobile Design"],
            status: "",
            category: "UX/UI"
        },
        {
            id: 7,
            title: "Explore India",
            subtitle: "Tourism Website Redesign",
            description: "A vibrant travel website redesign in Figma for Indian tourism, with responsive layouts that capture the feel of \"Incredible India.\"",
            shortDesc: "Showcasing India's incredible diversity",
            image: "/img/Explore India.png",
            link: "https://www.behance.net/gallery/201845335/Explore-India-A-traveling-website-inspired-by-India",
            type: "behance",
            technologies: ["Figma", "Responsive Design", "Cultural Design"],
            status: "",
            category: "UX/UI"
        }
    ]);

    function getProjectIcon(type: Project['type']) {
        switch(type) {
            case 'live': return '🌐';
            case 'github': return '⚙️';
            case 'figma': return '🎨';
            case 'behance': return '📱';
            default: return '🔗';
        }
    }

    function getProjectTypeLabel(type: Project['type']) {
        switch(type) {
            case 'live': return '';
            case 'github': return '';
            case 'figma': return 'Design Project';
            case 'behance': return 'Design Project';
            default: return '';
        }
    }
</script>

<template>
    <div class="projects-view">
        <div class="projects-header">
            <h1 class="projects-title">
                <span class="title-icon">🚀</span>
                <WobblyText text="Projects" :delay="0.08" />
            </h1>
            <p class="subtitle">Building things, breaking things, learning things</p>
        </div>

        <div class="projects-masonry">
            <div 
                v-for="(project, index) in projects" 
                :key="project.id" 
                class="project-card window"
                :class="{ 'card-offset': index % 2 === 1 }"
            >
                <div class="card-header">
                    <div class="project-section">
                        <div class="project-icon">{{ getProjectIcon(project.type) }}</div>
                        <div class="project-info">
                            <h3 class="project-name">
                                <WobblyText :text="project.title" :delay="0.03" />
                            </h3>
                            <p class="project-category">{{ project.category }}</p>
                        </div>
                    </div>
                    <div class="project-status" v-if="project.status">
                        <span class="status-badge" :class="project.type">{{ project.status }}</span>
                    </div>
                </div>
                
                <div class="card-content">
                    <!-- Project Image -->
                    <div class="project-image-section" v-if="project.image">
                        <div class="project-image">
                            <img :src="project.image" :alt="project.title" />
                            <div class="image-overlay">
                                <a 
                                    :href="project.link" 
                                    target="_blank" 
                                    rel="noopener noreferrer"
                                    class="overlay-link"
                                >
                                    View Project →
                                </a>
                            </div>
                        </div>
                    </div>
                    
                    <h4 class="project-subtitle">
                        <WobblyText :text="project.subtitle" :delay="0.02" />
                    </h4>
                    <p class="description">{{ project.shortDesc }}</p>
                    <p class="project-details">{{ project.description }}</p>
                    
                    <div class="tech-stack">
                        <span v-for="tech in project.technologies" :key="tech" class="tech-tag">
                            {{ tech }}
                        </span>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<!-- STYLES -->
<style scoped>
.projects-view {
  padding: 2rem;
  max-width: 1400px;
  margin: 0 auto;
}

.projects-header {
  text-align: center;
  margin-bottom: 3rem;
}

.projects-title {
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

.subtitle {
  font-size: clamp(1rem, 2.5vw, 1.2rem);
  color: var(--fg-light);
  opacity: 0.8;
  margin: 0.5rem 0 0 0;
  font-weight: 400;
}

.projects-masonry {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
  gap: 2rem;
  align-items: start;
}

.project-card {
  padding: 1.5rem;
  border-radius: 12px;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  background: var(--bg-secondary);
  border: 2px solid var(--fg-light);
  position: relative;
  animation: wobble 4s ease-in-out infinite;
}

@keyframes wobble {
  0%, 100% {
    transform: translateY(0px) rotate(0deg);
  }
  25% {
    transform: translateY(-5px) rotate(0.5deg);
  }
  50% {
    transform: translateY(3px) rotate(-0.3deg);
  }
  75% {
    transform: translateY(-3px) rotate(0.2deg);
  }
}

@keyframes wobble-offset {
  0%, 100% {
    transform: translateY(3px) rotate(0deg);
  }
  25% {
    transform: translateY(-3px) rotate(-0.3deg);
  }
  50% {
    transform: translateY(5px) rotate(0.4deg);
  }
  75% {
    transform: translateY(-2px) rotate(-0.2deg);
  }
}

.card-offset {
  margin-top: 2rem;
  animation: wobble-offset 4s ease-in-out infinite;
}

.project-card:hover {
  transform: translateY(-8px);
  scale: 1.05;
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

.project-section {
  display: flex;
  align-items: center;
  gap: 0.8rem;
  flex: 1;
}

.project-icon {
  width: 40px;
  height: 40px;
  border-radius: 8px;
  display: flex;
  align-items: center;
  justify-content: center;
  border: 2px solid rgba(134, 193, 252, 0.2);
  font-size: 1.2rem;
  transition: all 0.3s ease;
  background: linear-gradient(135deg, rgba(134, 193, 252, 0.05), rgba(134, 193, 252, 0.1));
}

.project-icon:hover {
  border-color: var(--color-accent);
  transform: scale(1.1);
}

.project-info {
  flex: 1;
}

.project-name {
  font-size: clamp(1.1rem, 2.5vw, 1.3rem);
  font-weight: 700;
  color: var(--color-accent);
  margin: 0;
  line-height: 1.2;
}

.project-category {
  font-size: clamp(0.75rem, 1.8vw, 0.85rem);
  color: var(--fg-light);
  opacity: 0.7;
  margin: 0.2rem 0 0 0;
}

.project-status {
  display: flex;
  align-items: center;
}

.status-badge {
  font-size: clamp(0.75rem, 1.8vw, 0.85rem);
  color: var(--fg-light);
  opacity: 0.8;
  font-weight: 500;
  text-align: right;
  white-space: nowrap;
  padding: 0.25rem 0.6rem;
  border-radius: 6px;
  border: 1px solid rgba(134, 193, 252, 0.25);
}

.status-badge.live {
  background: rgba(16, 185, 129, 0.1);
  color: #10b981;
  border-color: rgba(16, 185, 129, 0.3);
}

.status-badge.github {
  background: rgba(99, 102, 241, 0.1);
  color: #6366f1;
  border-color: rgba(99, 102, 241, 0.3);
}

.status-badge.figma,
.status-badge.behance {
  background: rgba(245, 158, 11, 0.1);
  color: #f59e0b;
  border-color: rgba(245, 158, 11, 0.3);
}

.card-content {
  border-top: 1px solid rgba(134, 193, 252, 0.15);
  padding-top: 1rem;
}

.project-image-section {
  margin-bottom: 1rem;
}

.project-image {
  border-radius: 8px;
  overflow: hidden;
  border: 2px solid rgba(134, 193, 252, 0.2);
  transition: all 0.3s ease;
  background: var(--bg-secondary);
  position: relative;
}

.project-image:hover {
  border-color: var(--color-accent);
  transform: translateY(-2px);
  box-shadow: 0 8px 20px rgba(134, 193, 252, 0.15);
}

.project-image img {
  width: 100%;
  height: 200px;
  object-fit: cover;
  display: block;
  transition: transform 0.3s ease;
}

.project-image:hover img {
  transform: scale(1.02);
}

.image-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(135deg, 
    rgba(0, 0, 0, 0.7), 
    rgba(134, 193, 252, 0.3));
  opacity: 0;
  transition: opacity 0.3s ease;
  display: flex;
  align-items: center;
  justify-content: center;
  backdrop-filter: blur(5px);
}

.project-image:hover .image-overlay {
  opacity: 1;
}

.overlay-link {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  color: white;
  text-decoration: none;
  font-weight: 600;
  font-size: clamp(0.9rem, 2vw, 1rem);
  padding: 0.6rem 1.2rem;
  border-radius: 25px;
  background: rgba(134, 193, 252, 0.9);
  transition: all 0.3s ease;
  transform: translateY(10px);
  backdrop-filter: blur(10px);
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.3);
}

.project-image:hover .overlay-link {
  transform: translateY(0);
}

.overlay-link:hover {
  background: var(--color-accent);
  transform: translateY(-3px);
  box-shadow: 0 8px 25px rgba(134, 193, 252, 0.4);
}

.project-subtitle {
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

.project-details {
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

/* Responsive Design */
@media screen and (max-width: 900px) {
  .projects-masonry {
    grid-template-columns: 1fr;
    gap: 1.5rem;
  }

  .card-offset {
    margin-top: 0;
    animation: wobble 4s ease-in-out infinite;
  }
}

@media screen and (max-width: 768px) {
  .projects-view {
    padding: 1rem;
  }
  
  .projects-header {
    margin-bottom: 2rem;
  }
  
  .project-card {
    padding: 1.2rem;
  }

  .card-header {
    flex-direction: column;
    align-items: flex-start;
    gap: 0.8rem;
  }

  .project-status {
    align-self: stretch;
    justify-content: flex-start;
  }

  .projects-title {
    flex-direction: column;
    gap: 0.5rem;
  }
}

@media screen and (max-width: 480px) {
  .projects-masonry {
    gap: 1rem;
  }

  .project-card {
    padding: 1rem;
  }

  .project-section {
    gap: 0.6rem;
  }

  .project-icon {
    width: 35px;
    height: 35px;
  }

  .tech-stack {
    gap: 0.3rem;
  }
}
</style>
