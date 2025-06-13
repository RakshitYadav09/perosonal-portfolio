<script setup lang="ts">
    import "@/assets/styles/info/base.css";
    // import WobblyText from "@/components/text/Wobbly.vue";

    // import ProjectCard from "@/components/info/ProjectCard.vue";
    /**IMAGES */
    // import ramlethal from "@/assets/img/ramlethal.webp";
    // import rubiu5Image from "@/assets/img/rubiu5.webp";
    // import archanImage from "@/assets/img/archan.webp";
    // import limeCordIcon from "@/assets/img/limecord.webp";
    // import ryokoIcon from "@/assets/img/ryoko.webp";
</script>

<template>
    <!-- <main class="flex col g-xxl">
        <h1 class="projects__title font-pixel text-title">
            <span>> </span>
            <WobblyText text="Projects" :delay="0.05" />
        </h1>

        <div class="projects__content">
            <div class="full-w flex j-center a-center">
                <img class="ramlethal-img" :src="ramlethal" />
                <h2>Still not much...</h2>
            </div>

            <div class="divider" />

            <div class="projects__list flex col g-m">
                <ProjectCard
                    title="Rubiu5"
                    description="Rubius's Discord bot, made in JavaScript."
                    :image="rubiu5Image"
                />
                <ProjectCard
                    title="Archan"
                    description="My own Discord bot coded in rust, rocking a control panel."
                    :image="archanImage"
                />
                <ProjectCard
                    title="LimeCord"
                    description="Lightweight frontend for Discord writen with Tauri."
                    :image="limeCordIcon"
                />
                <ProjectCard
                    title="Ryoko"
                    description="Performant Kotlin Minecraft plugin to replace EssentialsX."
                    :image="ryokoIcon"
                />
            </div>
        </div>
    </main> -->

    <main class="under-construction">
        <div class="construction-content">
            <div class="construction-icon">🚧</div>
            <h1 class="construction-title">Projects Under Construction</h1>
            <p class="construction-message">
                Currently working on some amazing projects! This showcase will be ready soon with all the cool stuff I've been building.
            </p>
            <div class="construction-animation">
                <div class="tool tool-1">🔨</div>
                <div class="tool tool-2">⚙️</div>
                <div class="tool tool-3">🔧</div>
                <div class="tool tool-4">📐</div>
            </div>
            <div class="progress-bar">
                <div class="progress-fill"></div>
            </div>
            <p class="progress-text">Building awesome projects... 42%</p>
        </div>
    </main>
</template>

<!-- STYLES -->
<style scoped>
    /* .ramlethal-img { height: clamp(7rem, 20dvw, 20rem) } */

    .under-construction {
        display: flex;
        align-items: center;
        justify-content: center;
        min-height: 80vh;
        padding: 2rem;
    }

    .construction-content {
        text-align: center;
        max-width: 600px;
    }

    .construction-icon {
        font-size: clamp(4rem, 12vw, 7rem);
        margin-bottom: 2rem;
        animation: bounce 2s infinite, rotate 8s linear infinite;
    }

    .construction-title {
        font-size: clamp(2.5rem, 6vw, 3.5rem);
        color: var(--color-accent);
        margin: 0 0 1.5rem 0;
        font-weight: 700;
        text-shadow: 0 0 20px rgba(134, 193, 252, 0.3);
    }

    .construction-message {
        font-size: clamp(1.1rem, 2.8vw, 1.3rem);
        color: var(--fg-light);
        opacity: 0.9;
        margin: 0 0 3rem 0;
        line-height: 1.6;
    }

    .construction-animation {
        display: flex;
        justify-content: center;
        gap: 2rem;
        margin: 2rem 0;
    }

    .tool {
        font-size: 2.5rem;
        animation: float 3s ease-in-out infinite;
    }

    .tool-1 {
        animation-delay: 0s;
    }

    .tool-2 {
        animation-delay: 0.5s;
        animation: spin 4s linear infinite;
    }

    .tool-3 {
        animation-delay: 1s;
    }

    .tool-4 {
        animation-delay: 1.5s;
    }

    .progress-bar {
        width: 100%;
        height: 8px;
        background: rgba(134, 193, 252, 0.1);
        border-radius: 4px;
        overflow: hidden;
        margin: 2rem 0 1rem 0;
        border: 1px solid rgba(134, 193, 252, 0.3);
    }

    .progress-fill {
        width: 42%;
        height: 100%;
        background: linear-gradient(90deg, var(--color-accent), rgba(134, 193, 252, 0.8));
        border-radius: 4px;
        animation: progress-glow 2s ease-in-out infinite alternate;
    }

    .progress-text {
        font-size: clamp(0.9rem, 2.2vw, 1rem);
        color: var(--color-accent);
        font-weight: 500;
        margin: 0;
        opacity: 0.8;
    }

    @keyframes bounce {
        0%, 20%, 50%, 80%, 100% {
            transform: translateY(0);
        }
        40% {
            transform: translateY(-20px);
        }
        60% {
            transform: translateY(-10px);
        }
    }

    @keyframes rotate {
        0% {
            transform: rotate(0deg);
        }
        100% {
            transform: rotate(360deg);
        }
    }

    @keyframes float {
        0%, 100% {
            transform: translateY(0px);
        }
        50% {
            transform: translateY(-15px);
        }
    }

    @keyframes spin {
        0% {
            transform: rotate(0deg);
        }
        100% {
            transform: rotate(360deg);
        }
    }

    @keyframes progress-glow {
        0% {
            box-shadow: 0 0 5px rgba(134, 193, 252, 0.5);
        }
        100% {
            box-shadow: 0 0 20px rgba(134, 193, 252, 0.8), 0 0 30px rgba(134, 193, 252, 0.4);
        }
    }

    @media screen and (max-width: 768px) {
        .under-construction {
            min-height: 70vh;
            padding: 1rem;
        }
        
        .construction-animation {
            gap: 1.5rem;
        }
        
        .tool {
            font-size: 2rem;
        }
    }

    @media screen and (max-width: 480px) {
        .construction-animation {
            gap: 1rem;
        }
        
        .tool {
            font-size: 1.5rem;
        }
    }
</style>