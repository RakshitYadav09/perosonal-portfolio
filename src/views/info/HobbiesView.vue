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
        gap: 2rem;
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
</style>