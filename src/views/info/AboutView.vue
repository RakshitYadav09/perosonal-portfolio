<script setup lang="ts">
    import "@/assets/styles/info/base.css";
    import WobblyText from "@/components/text/Wobbly.vue";
    import mayGif from "@/assets/animations/may_anggy.gif";
</script>

<template>
    <main class="flex col g-xxl">
        <h1 class="about__title font-pixel text-title">
            <span>> </span>
            <WobblyText text="About me" :delay="0.05" />
        </h1>

        <div class="about__content">
            <!-- Main content layout -->
            <div class="about__layout">
                <!-- Left side: Image and greeting -->
                <div class="about__left">
                    <img class="about__image" :src="mayGif" />
                    <div class="about__greeting">
                        <WobblyText text="Heya!" :delay="0.05" />
                        <br>
                        <WobblyText text="I am Rakshit" :delay="0.05" />
                    </div>
                </div>

                <!-- Right side: Text content -->
                <div class="about__right">
                    <p class="about__paragraph">
                        <WobblyText text="I'm a final year Computer Science student at SRM who likes to keep things interesting—one day I'm building web apps, the next I'm figuring out how to make stuff run (which i broke in the process btw). I have a soft spot for good design and love bringing ideas to life on Figma (I'd say I'm pretty handy with it too)." :delay="0" />
                    </p>
                    
                    <p class="about__paragraph">
                        <WobblyText text="When I'm not juggling projects or classes, you'll find me grinding away at LeetCode problems. It's a lot to balance, but I genuinely enjoy the challenge and learning something new every day." :delay="0" />
                    </p>
                    
                    <p class="about__paragraph">
                        <WobblyText text="Python and TS are my main programming languages, I am trying to find others that I like but I end up returning to these two... Always." :delay="0" />
                    </p>
                </div>
            </div>
        </div>
    </main>
</template>

<style scoped>
    .about__content {
        width: 100%;
    }

    .about__layout {
        display: grid;
        grid-template-columns: 1fr 2fr;
        gap: 3rem;
        align-items: start;
    }

    .about__left {
        display: flex;
        flex-direction: column;
        align-items: center;
        gap: 1.5rem;
    }

    .about__image {
        width: 100%;
        max-width: 250px;
        
    }

    .about__greeting {
        font-size: 2rem;
        font-weight: bold;
        text-align: center;
        color: var(--fg-light);
    }

    .about__right {
        display: flex;
        flex-direction: column;
        gap: 2rem;
    }

    .about__paragraph {
        font-size: 1.2rem;
        line-height: 1.6;
        color: var(--fg-light);
        margin: 0;
    }

    .about__paragraph :deep(.wobbly-text) {
        font-size: inherit;
        line-height: inherit;
    }

    @media screen and (max-width: 768px) {
        .about__layout {
            grid-template-columns: 1fr;
            gap: 2rem;
        }

        .about__left {
            justify-self: center;
        }

        .about__image {
            max-width: 200px;
        }

        .about__greeting {
            font-size: 1.2rem;
        }

        .about__paragraph {
            font-size: 0.85rem;
        }
    }
</style>