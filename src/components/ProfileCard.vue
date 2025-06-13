<script setup lang="ts">
    import { ref } from "vue";
    import WobblyText from "@/components/text/Wobbly.vue";

    import arrowIcon from "@/assets/svg/play.svg";
    import profileImage from "@/assets/img/Img_2025_06_14_01_30_52~2.jpeg";

    let idx = 0;
    let messageIndex = 0;
    let labelIndex = 0;

    let displayedMessage = ref("Heya! I am Rakshit, an aspiring software engineer that likes to design and develop cool stuff.");
    let displayedLabel = ref("Click to know more about me one line at a time");

    const messageList = [
    "Optimus Prime taught me that with great power comes great responsibility... and cool transformations.",
    "Cars are just computers with wheels now. I'm basically a car whisperer.",
    "I can center a div, but I can't center my life choices.",
    "Figma is my happy place. Photoshop is where dreams go to die.",
    "My code is like a McDonald's ice cream machine - it works sometimes.",
    "Transformers: More than meets the eye. My code: Less than meets the eye.",
    "I design websites like I design my room - organized chaos with good lighting.",
    "Bumblebee is the best Autobot, fight me.",
    "Megatron had the right idea about world domination, wrong approach though.",
    "Studio Ghibli taught me that even the smallest details matter in design.",
    "Naruto has fewer plot holes than my first JavaScript project.",
    "My freelance rate increases with each 'Can you make it look more professional?'",
    "Currently accepting job offers and emotional support in equal measure.",
    "Hire me and I'll debug your code AND play piano at the office party.",
    ]

    const labelList = [
    "Click me!",
    "Again!",
    "One more!",
    "Keep going!",
    "Don't stop!",
    "More facts!",
    "Hit me!",
    "Another one!",
    "Keep clicking!",
    "Fun fact time!",
    "Tell me more!",
    "What's next?",
    "Surprise me!",
    "I'm curious!",
    "Show me!",
    "Go on...",
    "Continue!",
    "More please!",
    "Keep it coming!",
    "Next fact!",
    "I want more!",
    "Don't stop now!",
    "Feed me facts!",
    "Keep the fun going!",
    "What else?",
    "Tell me another!",
    "I'm addicted!",
    "More wisdom!",
    "Keep sharing!",
    "Another gem!"
    ]

    const randomizeMessage = (): void => {
        // Randomize main message
        let randomMessageIndex = Math.floor(Math.random() * (messageList.length - 1));
        if (randomMessageIndex === messageIndex) {
            randomMessageIndex += 1;
        }
        messageIndex = randomMessageIndex;
        displayedMessage.value = messageList[randomMessageIndex];
        
        // Randomize label
        let randomLabelIndex = Math.floor(Math.random() * (labelList.length - 1));
        if (randomLabelIndex === labelIndex) {
            randomLabelIndex += 1;
        }
        labelIndex = randomLabelIndex;
        displayedLabel.value = labelList[randomLabelIndex];
        
        // Update index so the wobbly component re-renders
        idx += 1;
    }
</script>

<template>
    <button v-on:click="randomizeMessage" class="profile window full-w flex g-x p-x">
        <div class="profile__image-container">
            <img :src="profileImage" class="profile__image" alt="Profile picture">
        </div>

        <div class="textbox flex col g-m">
            <h1 class="profile__name">Rakshit Yadav</h1>
            <h1 class="profile__message adaptive-text-x">
                <WobblyText :text="displayedMessage" :key="idx" />
            </h1>
        </div>

        <div class="arrow-container">
            <div class="arrow-label-box">
                <span class="arrow-label">{{ displayedLabel }}</span>
            </div>
            <img class="arrow" :src="arrowIcon" alt="Click to change message" />
        </div>
    </button>
</template>

<style scoped>
    .profile {
        position: relative;
        background-color: transparent;
        text-align: left;
        align-items: stretch;
        min-height: 200px;
        transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
        overflow: hidden;
    }

    .profile:hover {
        transform: translateY(-4px);
        box-shadow: 0 12px 32px rgba(134, 193, 252, 0.2);
    }

    .profile__image-container {
        flex-shrink: 0;
        display: flex;
        align-items: center;
    }

    .profile__image {
        height: auto;
        width: clamp(6rem, 20dvw, 12rem);
        min-height: 100%;
        object-fit: cover;
        border-radius: 8px;
        transition: all 0.3s ease;
    }

    .profile:hover .profile__image {
        transform: scale(1.05);
        border-radius: 12px;
    }

    .profile__name {
        font-size: clamp(1.2rem, 4vw, 1.8rem);
        margin: 0;
        color: var(--color-accent);
        font-weight: 600;
    }

    .profile__message {
        font-size: clamp(0.9rem, 2.5vw, 1.1rem);
        line-height: 1.4;
        margin: 0;
    }

    .textbox {
        position: relative;
        padding-bottom: 3rem;
        flex: 1;
        overflow: hidden;
        justify-content: center;
        min-width: 0; /* Prevents flex item from overflowing */
    }

    .textbox:hover::before {
        content: "";
        position: absolute;
        left: -5rem;
        top: 0;
        height: 100%;
        width: 5rem;
        background-color: rgba(255, 255, 255, 0.249);
        transform: skewX(-15deg);
        animation: shine 3s cubic-bezier(0.23, 1, 0.320, 1) forwards;
    }

    .arrow-container {
        position: absolute;
        bottom: 1rem;
        right: 1rem;
        display: flex;
        align-items: center;
        gap: 0.8rem;
    }

    .arrow-label-box {
        background: rgba(134, 193, 252, 0.1);
        border: 1px solid rgba(134, 193, 252, 0.3);
        border-radius: 8px;
        padding: 0.5rem 0.8rem;
        backdrop-filter: blur(10px);
        transition: all 0.3s ease;
        box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
    }

    .profile:hover .arrow-label-box {
        background: rgba(134, 193, 252, 0.2);
        border-color: var(--color-accent);
        transform: translateY(-2px);
        box-shadow: 0 4px 12px rgba(134, 193, 252, 0.2);
    }

    .arrow-label {
        font-size: clamp(0.6rem, 1.8vw, 0.8rem);
        color: var(--fg-light);
        text-align: center;
        font-weight: 500;
        line-height: 1.2;
        white-space: nowrap;
        transition: all 0.3s ease;
        display: block;
    }

    .profile:hover .arrow-label {
        color: var(--color-accent);
    }

    .arrow {
        height: clamp(2.5rem, 8vw, 4rem);
        width: auto;
        animation: arrow-next 3s infinite linear;
        transition: all 0.3s ease;
        flex-shrink: 0;
    }

    .profile:hover .arrow {
        transform: scale(1.1);
        filter: brightness(1.2);
    }

    .animated-text {
        opacity: 0;
        position: relative;
        animation: wobbly 1s infinite linear, reveal .1s linear forwards;
    }

    @keyframes reveal {
        0% { opacity: 0; }
        100% { opacity: 1; }
    }

    @keyframes arrow-next {
        0% { right: 0; }
        50% { right: 0.5rem; }
        100% { right: 0; }
    }

    @keyframes wobbly {
        0% { bottom: 0; }
        50% { bottom: 2px; }
        100% { bottom: 0; }
    }

    @keyframes shine {
        0% {
            filter: blur(10px);
            left: -10rem;
            opacity: 0;
        }
        50% {
            filter: blur(0);
            opacity: 1;
        }
        100% {
            filter: blur(10px);
            left: 100%;
            opacity: 0;
        }
    }

    /* Responsive Design */
    @media screen and (max-width: 1024px) {
        .profile {
            min-height: 180px;
        }
        
        .profile__image {
            width: clamp(5rem, 18dvw, 10rem);
        }
    }

    @media screen and (max-width: 768px) {
        .profile {
            flex-direction: column;
            min-height: auto;
            text-align: center;
            padding: 1.5rem;
        }

        .profile__image-container {
            align-self: center;
            margin-bottom: 1rem;
        }

        .profile__image {
            width: clamp(8rem, 25dvw, 12rem);
        }

        .textbox {
            padding-bottom: 2rem;
            align-items: center;
        }

        .arrow-container {
            position: static;
            margin-top: 1rem;
            justify-content: center;
        }

        .arrow {
            height: clamp(2rem, 6vw, 3rem);
        }

        @keyframes arrow-next {
            0% { transform: translateY(0); }
            50% { transform: translateY(-0.5rem); }
            100% { transform: translateY(0); }
        }
    }

    @media screen and (max-width: 640px) {
        .profile {
            padding: 1rem;
        }

        .profile__image {
            width: clamp(6rem, 20dvw, 10rem);
        }

        .textbox {
            gap: 0.8rem;
        }

        .arrow-container {
            gap: 0.6rem;
        }

        .arrow-label-box {
            padding: 0.4rem 0.6rem;
        }

        .arrow-label {
            font-size: clamp(0.55rem, 1.6vw, 0.7rem);
        }
    }

    @media screen and (max-width: 480px) {
        .profile {
            padding: 0.8rem;
        }

        .profile__image {
            width: clamp(5rem, 18dvw, 8rem);
        }

        .textbox {
            gap: 0.6rem;
            padding-bottom: 1.5rem;
        }

        .arrow {
            height: clamp(1.5rem, 5vw, 2.5rem);
        }

        .arrow-container {
            gap: 0.4rem;
        }

        .arrow-label-box {
            padding: 0.3rem 0.5rem;
        }

        .arrow-label {
            font-size: clamp(0.5rem, 1.4vw, 0.65rem);
        }
    }
</style>