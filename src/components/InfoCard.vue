<script setup lang="ts">
    import { RouterLink } from "vue-router";

    defineProps({
        title:   String,
        iconUrl: String,
        path:    String,
    });
</script>

<template>
    <RouterLink :to="path ?? '/'" class="card window full-h full-w grid ratio-square p-x">
        <div class="img__container flex p-x">
            <img class="img full-h full-w" :src="iconUrl" alt="">
        </div>

        <h2 class="card-title adaptive-text-m overflow-hidden text-ellipsis">{{ title }}</h2>
    </RouterLink>
</template>

<style scoped>
    .card {
        grid-template-rows: 1fr auto;
        transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
        text-decoration: none;
        color: inherit;
        position: relative;
        overflow: hidden;
        min-height: clamp(120px, 22vw, 180px);
        aspect-ratio: 1;
        gap: clamp(0.2rem, 0.5vw, 0.4rem); /* Reduced gap between image and title */
    }

    .card::before {
        content: '';
        position: absolute;
        top: 0;
        left: -100%;
        width: 100%;
        height: 100%;
        background: linear-gradient(90deg, transparent, rgba(134, 193, 252, 0.1), transparent);
        transition: left 0.5s ease;
        z-index: 1;
    }

    .card:hover::before {
        left: 100%;
    }

    .card:hover {
        background-color: var(--fg-light);
        transform: translateY(-4px) scale(1.02);
        box-shadow: 0 8px 24px rgba(134, 193, 252, 0.2);
    }

    .card:hover .card-title {
        color: rgb(0, 0, 0);
    }

    .card:hover .img {
        filter: invert();
        transform: scale(1.1);
    }

    .card:active {
        transform: translateY(-2px) scale(1.01);
        transition: all 0.1s ease;
    }

    .img__container {
        padding: clamp(0.1rem, 0.5vw, 0.5rem); /* Increased padding for bigger images */
        display: flex;
        align-items: center;
        justify-content: center;
        flex: 1;
        min-height: 0;
    }

    .img {
        transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
        max-width: 100%; /* Increased from default to make image bigger */
        max-height: 100%; /* Increased from default to make image bigger */
        object-fit: contain;
        width: auto;
        height: auto;
    }

    .card-title {
        padding: clamp(0.3rem, 1vw, 0.5rem); /* Reduced padding */
        margin: 0;
        text-align: center;
        font-size: clamp(0.8rem, 2.5vw, 1.1rem);
        font-weight: 600;
        transition: all 0.3s ease;
        white-space: nowrap;
        overflow: hidden;
        text-overflow: ellipsis;
        position: relative;
        z-index: 2;
        color: var(--fg-light);
        background: transparent;
        display: block;
        flex-shrink: 0;
        min-height: auto;
        height: auto;
    }

    /* Responsive Design */
    @media screen and (max-width: 1024px) {
        .card {
            min-height: clamp(110px, 20vw, 160px);
            gap: clamp(0.15rem, 0.4vw, 0.3rem);
        }

        .img__container {
            padding: clamp(0.7rem, 2.2vw, 1.3rem);
        }

        .img {
            max-width: 80%;
            max-height: 80%;
        }
    }

    @media screen and (max-width: 768px) {
        .card {
            min-height: clamp(100px, 18vw, 140px);
            gap: clamp(0.1rem, 0.3vw, 0.25rem);
        }

        .card:hover {
            transform: translateY(-2px) scale(1.01);
        }

        .card-title {
            font-size: clamp(0.75rem, 2.2vw, 1rem);
            padding: clamp(0.25rem, 0.8vw, 0.4rem);
        }

        .img__container {
            padding: clamp(0.6rem, 2vw, 1.1rem);
        }

        .img {
            max-width: 75%;
            max-height: 75%;
        }
    }

    @media screen and (max-width: 640px) {
        .card {
            min-height: clamp(90px, 16vw, 120px);
            gap: clamp(0.1rem, 0.25vw, 0.2rem);
        }

        .card-title {
            font-size: clamp(0.7rem, 2vw, 0.9rem);
            padding: clamp(0.2rem, 0.7vw, 0.35rem);
        }

        .img__container {
            padding: clamp(0.5rem, 1.8vw, 1rem);
        }

        .img {
            max-width: 70%;
            max-height: 70%;
        }
    }

    @media screen and (max-width: 480px) {
        .card {
            min-height: clamp(80px, 14vw, 110px);
            gap: clamp(0.05rem, 0.2vw, 0.15rem);
        }

        .card-title {
            font-size: clamp(0.65rem, 1.8vw, 0.85rem);
            padding: clamp(0.2rem, 0.6vw, 0.3rem);
        }

        .card:hover {
            transform: translateY(-1px) scale(1.005);
        }

        .img__container {
            padding: clamp(0.4rem, 1.5vw, 0.8rem);
        }

        .img {
            max-width: 65%;
            max-height: 65%;
        }
    }

    @media screen and (max-width: 360px) {
        .card {
            min-height: clamp(70px, 12vw, 100px);
            gap: clamp(0.05rem, 0.15vw, 0.1rem);
        }

        .card-title {
            font-size: clamp(0.6rem, 1.5vw, 0.8rem);
            padding: clamp(0.15rem, 0.5vw, 0.25rem);
        }

        .img__container {
            padding: clamp(0.3rem, 1.2vw, 0.7rem);
        }

        .img {
            max-width: 60%;
            max-height: 60%;
        }
    }
</style>