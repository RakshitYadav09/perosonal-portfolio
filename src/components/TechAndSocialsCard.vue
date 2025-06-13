<script setup lang="ts">
    import { ref } from "vue";

    // Technologies - Updated icons
    import awsLogo from "@/assets/svg/aws-svgrepo-com.svg";
    import figmaLogo from "@/assets/svg/figma-svgrepo-com.svg";
    import mongodbLogo from "@/assets/svg/mongodb-opened-svgrepo-com.svg";
    import dockerLogo from "@/assets/svg/docker.svg";
    import vueLogo from "@/assets/svg/vue.svg";
    import gitLogo from "@/assets/svg/git.svg";
    import linuxLogo from "@/assets/svg/linux.svg";
    
    // Socials
    import githubLogo from "@/assets/svg/github.svg";
    import twitterLogo from "@/assets/svg/twitter.svg";
    import youtubeLogo from "@/assets/svg/youtube.svg";
    import discordLogo from "@/assets/svg/discord.svg";

    let showSocials = ref(false);
</script>

<template>
    <div class="window langs-and-socials grid slide-up-initial">
        <div class="selector grid g-x">
            <button
                :class="showSocials.valueOf() ? 'inactive' : 'active'"
                @click="showSocials = false"
                class="tab-button"
            >
                <h2 class="tab-title">Tech</h2>
            </button>

            <button
                :class="showSocials.valueOf() ? 'active' : 'inactive'"
                @click="showSocials = true"
                class="tab-button"
            >
                <h2 class="tab-title">Socials</h2>
            </button>
        </div>

        <!-- TECHNOLOGIES I USE -->
        <Transition name="slide-bottom" mode="out-in">
            <div v-if="!showSocials" class="content full-h full-w" key="tech">
                <div class="item-list flex g-xxl j-center wrap p-x">
                    <!-- AWS -->
                    <div class="item-wrapper">
                        <img class="item" :src="awsLogo" alt="Amazon Web Services logo">
                    </div>
                    
                    <!-- Figma -->
                    <div class="item-wrapper">
                        <img class="item" :src="figmaLogo" alt="Figma logo">
                    </div>
                    
                    <!-- React (using devicon) -->
                    <div class="item-wrapper tech-icon">
                        <i class="devicon-react-original colored"></i>
                    </div>
                    
                    <!-- MongoDB -->
                    <div class="item-wrapper">
                        <img class="item" :src="mongodbLogo" alt="MongoDB logo">
                    </div>
                    
                    <!-- Python (using devicon) -->
                    <div class="item-wrapper tech-icon">
                        <i class="devicon-python-plain colored"></i>
                    </div>
                    
                    <!-- Docker -->
                    <div class="item-wrapper">
                        <img class="item" :src="dockerLogo" alt="Docker logo">
                    </div>
                    
                    <!-- Git -->
                    <div class="item-wrapper">
                        <img class="item" :src="gitLogo" alt="Git logo">
                    </div>
                </div>
            </div>

            <!-- SOCIALS -->
            <div v-else class="content full-h full-w" key="socials">
                <div class="item-list flex g-xxl j-center wrap p-x">
                    <div class="item-wrapper">
                        <a href="https://github.com/notKimu" target="_blank" class="social-link">
                            <img class="item" :src="githubLogo" alt="Kimu's Github page">
                        </a>
                    </div>
                    <div class="item-wrapper">
                        <a href="https://twitter.com/notkimu" target="_blank" class="social-link">
                            <img class="item" :src="twitterLogo" alt="Kimu's Twitter page">
                        </a>
                    </div>
                    <div class="item-wrapper">
                        <a href="https://www.youtube.com/@kimu_x64" target="_blank" class="social-link">
                            <img class="item" :src="youtubeLogo" alt="Kimu's Youtube channel">
                        </a>
                    </div>
                    <div class="item-wrapper">
                        <a href="https://discord.gg/NfeXrQdXdE" target="_blank" class="social-link">
                            <img class="item" :src="discordLogo" alt="Kimu's Discord server">
                        </a>
                    </div>
                </div>
            </div>
        </Transition>
    </div>
</template>

<style scoped>
    /* Initial slide up animation for the whole card */
    @keyframes slideUpFromBottom {
        from {
            opacity: 0;
            transform: translateY(50px);
        }
        to {
            opacity: 1;
            transform: translateY(0);
        }
    }

    .slide-up-initial {
        animation: slideUpFromBottom 0.8s ease-out;
    }

    .langs-and-socials {
        grid-template-rows: auto 1fr;
        gap: 0;
        min-height: 200px;
    }

    .selector {
        border-bottom: var(--border-width) solid var(--fg-light);
        grid-template-columns: 1fr 1fr;
        gap: 0;
    }

    .tab-button {
        padding: 0.8rem 1rem;
        transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
        position: relative;
        overflow: hidden;
        margin: 0;
        border: none;
        background: transparent;
        cursor: pointer;
    }

    .tab-title {
        margin: 0;
        padding: 0;
        font-size: clamp(1.5rem, 3vw, 1.2rem);
        transition: all 0.3s ease;
    }

    .tab-button.active {
        background-color: var(--fg-light);
        transform: translateY(0px);
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    }

    .tab-button.active * {
        color: var(--bg-dark);
    }

    .tab-button.inactive {
        opacity: 0.7;
        transform: translateY(0);
    }

    .tab-button::before {
        content: '';
        position: absolute;
        top: 0;
        left: -100%;
        width: 100%;
        height: 100%;
        background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.1), transparent);
        transition: left 0.5s ease;
    }

    .tab-button:hover::before {
        left: 100%;
    }

    .tab-button:hover {
        transform: translateY(-3px);
        box-shadow: 0 6px 12px rgba(0, 0, 0, 0.15);
        background-color: var(--fg-light);
    }

    .tab-button:hover * {
        color: var(--bg-dark);
    }

    .tab-button:active {
        transform: translateY(-1px);
        transition: all 0.1s ease;
    }

    .content {
        padding: 1rem;
        margin: 0;
        display: flex;
        align-items: center;
        justify-content: center;
        min-height: 100px;
    }

    .item-list {
        width: 100%;
        justify-content: center;
        align-items: center;
        gap: clamp(1rem, 4vw, 2rem);
    }

    .item-wrapper {
        display: flex;
        align-items: center;
        justify-content: center;
        padding: 0.5rem;
        border-radius: 8px;
        transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
    }

    .item-wrapper:hover {
        /* background: rgba(134, 193, 252, 0.1); */
        transform: translateY(-4px);
    }

    .item {
        height: clamp(2.5rem, 8vw, 4rem);
        width: 70px;
        filter: saturate(0) brightness(0.8);
        transition: all 0.3s ease;
    }
    
    .item:hover {
        filter: none;
        transform: scale(1.3);
    }

    .social-link {
        display: block;
        text-decoration: none;
    }

    .tech-icon {
        cursor: pointer;
    }

    .tech-icon i {
        font-size: clamp(3.5rem, 10vw, 4rem);
        filter: saturate(0) brightness(0.8);
        transition: all 0.3s ease;
    }

    .tech-icon:hover i {
        filter: none;
        transform: scale(1.1);
    }

    /* Slide transitions from bottom */
    .slide-bottom-enter-active,
    .slide-bottom-leave-active {
        transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
    }

    .slide-bottom-enter-from {
        opacity: 0;
        transform: translateY(30px);
    }

    .slide-bottom-leave-to {
        opacity: 0;
        transform: translateY(-30px);
    }

    .slide-bottom-enter-to,
    .slide-bottom-leave-from {
        opacity: 1;
        transform: translateY(0);
    }

    /* Responsive Design */
    @media screen and (max-width: 1024px) {
        .content {
            padding: 1.2rem;
        }

        .item-list {
            gap: clamp(0.8rem, 3vw, 1.5rem);
        }
    }

    @media screen and (max-width: 768px) {
        .langs-and-socials {
            min-height: 250px;
        }

        .content {
            padding: 1rem;
            min-height: 150px;
        }

        .tab-button {
            padding: 0.6rem 0.8rem;
        }

        .item-list {
            gap: clamp(0.6rem, 2.5vw, 1.2rem);
        }

        .item-wrapper {
            padding: 0.3rem;
        }
    }

    @media screen and (max-width: 640px) {
        .langs-and-socials {
            min-height: 220px;
        }

        .content {
            padding: 0.8rem;
            min-height: 120px;
        }

        .tab-button {
            padding: 0.5rem 0.6rem;
        }

        .item-list {
            gap: clamp(0.5rem, 2vw, 1rem);
            flex-wrap: wrap;
            justify-content: center;
        }
    }

    @media screen and (max-width: 480px) {
        .langs-and-socials {
            min-height: 200px;
        }

        .content {
            padding: 0.6rem;
            min-height: 100px;
        }

        .tab-button {
            padding: 0.4rem 0.5rem;
        }

        .item-list {
            gap: clamp(0.4rem, 1.5vw, 0.8rem);
        }

        .item-wrapper {
            padding: 0.2rem;
        }
    }
</style>