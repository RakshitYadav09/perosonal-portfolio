<script setup lang="ts">
    import "@/assets/styles/info/base.css";
    import WobblyText from "@/components/text/Wobbly.vue";

    import sonicCorriendoGif from "@/assets/animations/sonic-corriendo.gif";
</script>

<template>
    <main class="flex col g-xxl">
        <h1 class="hobbies__title font-pixel text-title">
            <span>> </span>
            <WobblyText text="Hobbies" :delay="0.05" />
        </h1>

        <main class="hobbies__content grid g-x">
            <div class="hobbies__content__sideimage">
                <img :src="sonicCorriendoGif" alt="Sonic running" />
            </div>

            <h3 class="hobbies__content__text white-text">
                <WobblyText text="Love music, cars, tech and watch a lot of racing. I like Pokemon too. I play the piano too sometimes (rare but I'm good at it)." :delay="0.01" />
                <br><br>
                <WobblyText text="I still really dont know how to fill up this section AJHKFJDVKJHFKJASHDKJHF" :delay="0.01" />
                <br><br><br>
                <WobblyText text="o(*￣▽￣*)ブ" :delay="0.05" />
            </h3>
        </main>
    </main>
</template>

<!-- STYLES -->
<style scoped>
    .hobbies__content {
        grid-template-columns: auto 1fr;
        align-items: start;
        gap: clamp(1rem, 4vw, 2rem);
    }
    
    .hobbies__content__sideimage { 
        width: clamp(8rem, 30dvw, 15rem);
        display: flex;
        justify-content: flex-start;
        align-items: flex-start;
    }

    .hobbies__content__sideimage img {
        width: 100%;
        height: auto;
        max-width: none;
        border-radius: 8px;
    }

    .hobbies__content__text {
        font-size: clamp(0.9rem, 2.5vw, 1.1rem);
        line-height: 1.6;
    }

    .white-text {
        color: rgb(157, 209, 255) !important;
    }

    .white-text .wobbly-text {
        color: rgb(157, 209, 255) !important;
    }

    .white-text :deep(.wobbly-text) {
        color: rgb(157, 209, 255) !important;
    }

    /* Tablet styles */
    @media screen and (max-width: 1024px) {
        .hobbies__content {
            gap: clamp(0.8rem, 3vw, 1.5rem);
        }
        
        .hobbies__content__sideimage { 
            width: clamp(7rem, 25dvw, 12rem);
        }

        .hobbies__content__text {
            font-size: clamp(0.85rem, 2.3vw, 1rem);
        }
    }

    /* Mobile landscape */
    @media screen and (max-width: 768px) {
        .hobbies__content {
            grid-template-columns: 1fr;
            gap: clamp(1rem, 4vw, 1.5rem);
            text-align: center;
        }
        
        .hobbies__content__sideimage { 
            width: clamp(6rem, 40vw, 10rem);
            justify-self: center;
            margin: 0 auto;
        }

        .hobbies__content__text {
            font-size: clamp(0.9rem, 2.8vw, 1.1rem);
            text-align: left;
        }

        .flex.col.g-xxl {
            gap: clamp(1.5rem, 5vw, 2rem);
        }
    }

    /* Mobile portrait */
    @media screen and (max-width: 480px) {
        .hobbies__content {
            gap: clamp(0.8rem, 3vw, 1.2rem);
        }
        
        .hobbies__content__sideimage { 
            width: clamp(5rem, 35vw, 8rem);
        }

        .hobbies__content__text {
            font-size: clamp(0.8rem, 2.5vw, 1rem);
            line-height: 1.5;
        }

        .hobbies__title {
            font-size: clamp(1.8rem, 6vw, 2.5rem);
        }

        .flex.col.g-xxl {
            gap: clamp(1rem, 4vw, 1.5rem);
        }
    }

    /* Very small screens */
    @media screen and (max-width: 320px) {
        .hobbies__content__sideimage { 
            width: clamp(4rem, 30vw, 6rem);
        }

        .hobbies__content__text {
            font-size: clamp(0.75rem, 2.2vw, 0.9rem);
        }

        .hobbies__title {
            font-size: clamp(1.5rem, 5vw, 2rem);
        }
    }
</style>