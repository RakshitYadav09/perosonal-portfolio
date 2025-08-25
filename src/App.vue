<script setup lang="ts">
  import { RouterLink, RouterView, useRoute } from "vue-router";
  import { ref, onMounted, computed } from "vue";

  const route = useRoute();
  
  // Check if current route is projects page
  const isProjectsPage = computed(() => route.path === '/projects');

  let clickCounter = 0;
  function addClick() {
    clickCounter += 1;
  }

  // Random icon selection on page load
  const iconType = ref(Math.floor(Math.random() * 3)); // 0, 1, or 2

  // Add mobile menu state
  const showMobileMenu = ref(false);

  const toggleMobileMenu = () => {
    showMobileMenu.value = !showMobileMenu.value;
  };

  // Close mobile menu when clicking outside or on links
  const closeMobileMenu = () => {
    showMobileMenu.value = false;
  };

  // --- START: Music Player Integration ---
  import lobbyMusicFile from "@/assets/audio/lobby_music.mp3";

  const audioPlayer = ref<HTMLAudioElement | null>(null);
  const isMusicPlaying = ref(false);
  const isMusicMuted = ref(false);
  const volume = ref(60);
  const showMusicPlayer = ref(false);

  onMounted(() => {
    audioPlayer.value = new Audio(lobbyMusicFile);
    audioPlayer.value.loop = true;
    audioPlayer.value.volume = volume.value / 100;
    
    // Event listeners for audio state changes
    if (audioPlayer.value) {
      audioPlayer.value.addEventListener('play', () => {
        isMusicPlaying.value = true;
      });
      
      audioPlayer.value.addEventListener('pause', () => {
        isMusicPlaying.value = false;
      });
    }
  });

  const toggleMusic = () => {
    if (audioPlayer.value) {
      if (isMusicPlaying.value) {
        audioPlayer.value.pause();
      } else {
        audioPlayer.value.play();
      }
    }
  };

  const toggleMute = () => {
    if (audioPlayer.value) {
      audioPlayer.value.muted = !audioPlayer.value.muted;
      isMusicMuted.value = audioPlayer.value.muted;
    }
  };

  const changeVolume = (event: Event) => {
    const target = event.target as HTMLInputElement;
    volume.value = parseInt(target.value);
    if (audioPlayer.value) {
      audioPlayer.value.volume = volume.value / 100;
    }
  };

  const toggleMusicPlayer = () => {
    showMusicPlayer.value = !showMusicPlayer.value;
  };
  // --- END: Music Player Integration ---
</script>

<!-- Content -->
<template>
  <div class="global__container">
    <header>
      <div class="header__content" v-if="!showMusicPlayer">
        <RouterLink to="/">
          <button class="header__logo flex a-center g-m" v-on:click="addClick()">
            <div class="icon__container">
              <!-- Computer Monitor Icon -->
              <svg v-if="iconType === 0" class="full-h" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                <rect x="2" y="3" width="20" height="14" rx="2" stroke="rgb(134, 193, 252)" stroke-width="2" fill="none"/>
                <rect x="4" y="5" width="16" height="10" fill="rgb(134, 193, 252)" opacity="0.2"/>
                <rect x="8" y="18" width="8" height="2" fill="rgb(134, 193, 252)"/>
                <rect x="6" y="20" width="12" height="1" fill="rgb(134, 193, 252)"/>
                <circle cx="12" cy="10" r="1" fill="rgb(134, 193, 252)"/>
                <rect x="6" y="7" width="4" height="1" fill="rgb(134, 193, 252)"/>
                <rect x="6" y="9" width="3" height="1" fill="rgb(134, 193, 252)"/>
                <rect x="6" y="11" width="5" height="1" fill="rgb(134, 193, 252)"/>
                <rect x="6" y="13" width="2" height="1" fill="rgb(134, 193, 252)"/>
              </svg>
              
              <!-- Terminal Icon -->
              <svg v-else-if="iconType === 1" class="full-h" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                <rect x="3" y="4" width="18" height="12" rx="1" stroke="rgb(134, 193, 252)" stroke-width="2" fill="none"/>
                <rect x="5" y="6" width="14" height="8" fill="rgb(134, 193, 252)" opacity="0.1"/>
                <path d="M7 8L9 10L7 12" stroke="rgb(134, 193, 252)" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
                <rect x="11" y="11" width="4" height="1" fill="rgb(134, 193, 252)"/>
                <rect x="8" y="17" width="8" height="1.5" fill="rgb(134, 193, 252)"/>
                <rect x="6" y="19" width="12" height="1" fill="rgb(134, 193, 252)"/>
              </svg>
              
              <!-- Code Icon -->
              <svg v-else class="full-h" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M7 8L3 12L7 16" stroke="rgb(134, 193, 252)" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                <path d="M17 8L21 12L17 16" stroke="rgb(134, 193, 252)" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                <path d="M14 4L10 20" stroke="rgb(134, 193, 252)" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
              </svg>
            </div>
            <h1 class="logo-text">rezz:~$</h1>
          </button>
        </RouterLink>

        <!-- Desktop Navigation -->
        <nav class="header__nav desktop-nav">
          <RouterLink to="/about" class="nav__link">About</RouterLink>
          <RouterLink to="/projects" class="nav__link">Projects</RouterLink>
          <RouterLink to="/experience" class="nav__link">Experience</RouterLink>
          <RouterLink to="/hobbies" class="nav__link">Hobbies</RouterLink>
          <a href="https://drive.google.com/file/d/16Fd0xVBjG2LaHxP9qs_8JB3QZCS7pswt/view?usp=sharing" 
             target="_blank" 
             rel="noopener noreferrer" 
             class="nav__link">
            Resume
          </a>
          <button @click="toggleMusicPlayer" class="music-toggle-btn">
            <span class="music-icon">♪</span>
          </button>
        </nav>

        <!-- Mobile Navigation -->
        <div class="mobile-nav">
          <button @click="toggleMusicPlayer" class="music-toggle-btn mobile-music-btn">
            <span class="music-icon">♪</span>
          </button>
          <button @click="toggleMobileMenu" class="mobile-menu-btn" :class="{ active: showMobileMenu }">
            <span class="hamburger-line"></span>
            <span class="hamburger-line"></span>
            <span class="hamburger-line"></span>
          </button>
        </div>

        <!-- Mobile Dropdown Menu -->
        <div class="mobile-dropdown" :class="{ show: showMobileMenu }" @click="closeMobileMenu">
          <nav class="mobile-dropdown-nav">
            <RouterLink to="/about" class="mobile-nav__link" @click="closeMobileMenu">About</RouterLink>
            <RouterLink to="/projects" class="mobile-nav__link" @click="closeMobileMenu">Projects</RouterLink>
            <RouterLink to="/experience" class="mobile-nav__link" @click="closeMobileMenu">Experience</RouterLink>
            <RouterLink to="/hobbies" class="mobile-nav__link" @click="closeMobileMenu">Hobbies</RouterLink>
            <a href="https://drive.google.com/file/d/16Fd0xVBjG2LaHxP9qs_8JB3QZCS7pswt/view?usp=sharing" 
               target="_blank" 
               rel="noopener noreferrer" 
               class="mobile-nav__link"
               @click="closeMobileMenu">
              Resume
            </a>
          </nav>
        </div>
      </div>

      <!-- Enhanced Music Player Header -->
      <div class="music-header__content" v-if="showMusicPlayer">
        <div class="music-controls">
          <button @click="toggleMusicPlayer" class="retro-button close-btn">
            <span>×</span>
          </button>
          
          <button @click="toggleMusic" class="retro-button play-btn" :class="{ active: isMusicPlaying }">
            <span v-if="isMusicPlaying">⏸</span>
            <span v-else>▶</span>
          </button>
          
          <button @click="toggleMute" class="retro-button mute-btn" :class="{ active: isMusicMuted }">
            <span v-if="isMusicMuted">🔇</span>
            <span v-else>🔊</span>
          </button>
          
          <div class="volume-control">
            <span class="volume-label">VOL</span>
            <input 
              type="range" 
              min="0" 
              max="100" 
              :value="volume" 
              @input="changeVolume"
              class="volume-slider"
              :disabled="isMusicMuted"
            />
            <span class="volume-text">{{ isMusicMuted ? 'MUTE' : volume + '%' }}</span>
          </div>
          
          <div class="music-status">
            <div class="status-indicator" :class="{ active: isMusicPlaying }"></div>
            <span class="status-text">{{ isMusicPlaying ? 'PLAYING' : 'PAUSED' }}</span>
          </div>
        </div>
      </div>
    </header>
    <div class="filler" />

    <RouterView />
  </div>

  <div class="retro-overlay screen-h screen-w" :class="{ 'hidden-on-projects': isProjectsPage }" />
</template>

<!-- Styles -->
<style scoped>
  header {
    height: clamp(3rem, 8vw, 3.5rem);
    width: 100dvw;
    position: fixed;
    background: linear-gradient(135deg, #000000 0%, #1a1a1a 100%);
    border-bottom: 2px solid var(--fg-light);
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.5);
    z-index: 999;
    animation: slideDownFromTop 0.8s ease-out;
  }

  @keyframes slideDownFromTop {
    from {
      opacity: 0;
      transform: translateY(-100%);
    }
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }

  .header__content {
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 0 clamp(0.5rem, 4vw, 2rem);
    max-width: 1400px;
    margin: 0 auto;
  }

  .header__logo {
    height: 100%;
    background: none;
    border: none;
    cursor: pointer;
    color: var(--fg-light);
    transition: all 0.3s ease;
    padding: 0.5rem;
  }

  .header__logo:hover {
    transform: scale(1.05);
    color: var(--color-accent);
  }

  .icon__container {
    height: clamp(1.5rem, 6vw, 2.2rem);
    flex-shrink: 0;
  }

  .logo-text {
    font-size: clamp(0.9rem, 3.5vw, 1.2rem);
    margin: 0;
    margin-left: 0.5rem;
  }

  .header__nav {
    display: flex;
    align-items: center;
    gap: clamp(0.3rem, 2vw, 1.2rem);
    flex-wrap: nowrap;
    overflow-x: auto;
    scrollbar-width: none;
    -ms-overflow-style: none;
  }

  .header__nav::-webkit-scrollbar {
    display: none;
  }

  .nav__link {
    color: var(--fg-light);
    text-decoration: none;
    font-size: clamp(0.65rem, 2.2vw, 0.95rem);
    font-weight: 500;
    padding: clamp(0.25rem, 1.5vw, 0.6rem) clamp(0.4rem, 2.5vw, 1.2rem);
    border-radius: 6px;
    transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
    position: relative;
    border: 1px solid transparent;
    white-space: nowrap;
    flex-shrink: 0;
  }

  .nav__link:hover {
    background: rgba(134, 193, 252, 0.15);
    color: var(--color-accent);
    border-color: rgba(134, 193, 252, 0.3);
    transform: translateY(-2px);
    box-shadow: 0 4px 12px rgba(134, 193, 252, 0.2);
  }

  .nav__link.router-link-active {
    color: var(--color-accent);
    background: rgba(134, 193, 252, 0.2);
    border-color: var(--color-accent);
  }

  .music-toggle-btn {
    background: linear-gradient(135deg, #1a1a1a 0%, #2a2a2a 100%);
    color: var(--fg-light);
    border: 2px solid var(--fg-light);
    padding: clamp(0.4rem, 1.5vw, 0.6rem);
    font-size: clamp(12px, 4vw, 18px);
    cursor: pointer;
    transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
    width: clamp(30px, 10vw, 42px);
    height: clamp(30px, 10vw, 42px);
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 8px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.3);
    flex-shrink: 0;
  }

  .music-toggle-btn:hover {
    background: var(--color-accent);
    color: black;
    transform: translateY(-3px) scale(1.05);
    box-shadow: 0 6px 20px rgba(134, 193, 252, 0.4);
    border-color: var(--color-accent);
  }

  .music-icon {
    animation: musicNote 2s ease-in-out infinite;
  }

  @keyframes musicNote {
    0%, 100% { transform: scale(1); }
    50% { transform: scale(1.1); }
  }

  .music-toggle-btn:hover .music-icon {
    animation: musicNoteFast 0.5s ease-in-out infinite;
  }

  @keyframes musicNoteFast {
    0%, 100% { transform: scale(1) rotate(0deg); }
    25% { transform: scale(1.15) rotate(-8deg); }
    75% { transform: scale(1.15) rotate(8deg); }
  }

  /* Mobile Navigation Styles */
  .desktop-nav {
    display: flex;
  }

  .mobile-nav {
    display: none;
    align-items: center;
    gap: 0.5rem;
  }

  .mobile-music-btn {
    background: linear-gradient(135deg, #1a1a1a 0%, #2a2a2a 100%);
    color: var(--fg-light);
    border: 2px solid var(--fg-light);
    padding: 0.4rem;
    font-size: 14px;
    cursor: pointer;
    transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
    width: 35px;
    height: 35px;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 6px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.3);
  }

  .mobile-menu-btn {
    background: linear-gradient(135deg, #1a1a1a 0%, #2a2a2a 100%);
    color: var(--fg-light);
    border: 2px solid var(--fg-light);
    cursor: pointer;
    transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
    width: 40px;
    height: 35px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    border-radius: 6px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.3);
    gap: 3px;
    padding: 0;
  }

  .mobile-menu-btn:hover,
  .mobile-music-btn:hover {
    background: var(--color-accent);
    color: black;
    transform: translateY(-2px) scale(1.05);
    box-shadow: 0 4px 16px rgba(134, 193, 252, 0.4);
    border-color: var(--color-accent);
  }

  .hamburger-line {
    width: 20px;
    height: 2px;
    background: currentColor;
    transition: all 0.3s ease;
    border-radius: 1px;
  }

  .mobile-menu-btn.active .hamburger-line:nth-child(1) {
    transform: rotate(45deg) translate(5px, 5px);
  }

  .mobile-menu-btn.active .hamburger-line:nth-child(2) {
    opacity: 0;
  }

  .mobile-menu-btn.active .hamburger-line:nth-child(3) {
    transform: rotate(-45deg) translate(7px, -6px);
  }

  .mobile-dropdown {
    position: absolute;
    top: 100%;
    left: 0;
    right: 0;
    background: linear-gradient(135deg, #000000 0%, #1a1a1a 100%);
    border-bottom: 2px solid var(--fg-light);
    box-shadow: 0 8px 24px rgba(0, 0, 0, 0.5);
    transform: translateY(-100%);
    opacity: 0;
    visibility: hidden;
    transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
    z-index: 998;
  }

  .mobile-dropdown.show {
    transform: translateY(0);
    opacity: 1;
    visibility: visible;
  }

  .mobile-dropdown-nav {
    display: flex;
    flex-direction: column;
    padding: 1rem;
    gap: 0.5rem;
    max-width: 1400px;
    margin: 0 auto;
  }

  .mobile-nav__link {
    color: var(--fg-light);
    text-decoration: none;
    font-size: 1rem;
    font-weight: 500;
    padding: 1rem 1.5rem;
    border-radius: 8px;
    transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
    border: 1px solid transparent;
    text-align: center;
    background: rgba(134, 193, 252, 0.05);
  }

  .mobile-nav__link:hover {
    background: rgba(134, 193, 252, 0.15);
    color: var(--color-accent);
    border-color: rgba(134, 193, 252, 0.3);
    transform: translateY(-2px);
    box-shadow: 0 4px 12px rgba(134, 193, 252, 0.2);
  }

  .mobile-nav__link.router-link-active {
    color: var(--color-accent);
    background: rgba(134, 193, 252, 0.2);
    border-color: var(--color-accent);
  }

  /* Enhanced Music Player Header Styles */
  .music-header__content {
    height: 100%;
    padding: 0 clamp(0.5rem, 4vw, 2rem);
    display: flex;
    align-items: center;
  }

  .music-controls {
    display: flex;
    align-items: center;
    gap: clamp(6px, 3vw, 16px);
    width: 100%;
    max-width: 1400px;
    margin: 0 auto;
    overflow-x: auto;
    padding: 0.5rem 0;
    scrollbar-width: none;
    -ms-overflow-style: none;
  }

  .music-controls::-webkit-scrollbar {
    display: none;
  }

  .retro-button {
    background: linear-gradient(135deg, #1a1a1a 0%, #2a2a2a 100%);
    color: var(--fg-light);
    border: 2px solid var(--fg-light);
    padding: clamp(6px, 2vw, 12px);
    font-size: clamp(10px, 3vw, 14px);
    cursor: pointer;
    transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
    min-width: clamp(30px, 8vw, 40px);
    height: clamp(30px, 8vw, 40px);
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 6px;
    font-weight: 600;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.3);
    flex-shrink: 0;
  }

  .retro-button:hover {
    background: var(--fg-light);
    color: black;
    transform: translateY(-2px) scale(1.05);
    box-shadow: 0 4px 16px rgba(134, 193, 252, 0.3);
  }

  .retro-button:active {
    transform: translateY(0) scale(0.98);
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.3);
  }

  .retro-button.active {
    background: #1e3a8a;
    color: white;
    border-color: #1e3a8a;
    box-shadow: 0 0 16px rgba(30, 58, 138, 0.5);
  }

  .retro-button.active:hover {
    background: #1e3a8a;
    color: white;
    filter: brightness(1.1);
  }

  .close-btn {
    font-size: clamp(16px, 4vw, 20px);
    font-weight: bold;
    background: linear-gradient(135deg, #dc2626 0%, #ef4444 100%);
    border-color: #dc2626;
  }

  .close-btn:hover {
    background: #dc2626;
    border-color: #dc2626;
    color: white;
  }

  .volume-control {
    display: flex;
    align-items: center;
    gap: clamp(6px, 2.5vw, 12px);
    padding: clamp(4px, 2vw, 8px) clamp(8px, 3.5vw, 16px);
    background: rgba(134, 193, 252, 0.1);
    border: 1px solid rgba(134, 193, 252, 0.3);
    border-radius: 8px;
    flex-shrink: 0;
    min-width: clamp(90px, 25vw, 160px);
  }

  .volume-label {
    font-size: clamp(8px, 2vw, 10px);
    color: var(--color-accent);
    font-weight: bold;
    letter-spacing: 1px;
    font-family: 'Courier New', monospace;
  }

  .volume-slider {
    width: clamp(40px, 15vw, 100px);
    height: 6px;
    background: #2a2a2a;
    outline: none;
    border: 1px solid var(--fg-light);
    cursor: pointer;
    border-radius: 3px;
    appearance: none;
  }

  .volume-slider::-webkit-slider-thumb {
    appearance: none;
    width: clamp(12px, 4vw, 16px);
    height: clamp(12px, 4vw, 16px);
    background: var(--color-accent);
    cursor: pointer;
    border: 2px solid black;
    border-radius: 50%;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
  }

  .volume-slider::-moz-range-thumb {
    width: clamp(12px, 4vw, 16px);
    height: clamp(12px, 4vw, 16px);
    background: var(--color-accent);
    cursor: pointer;
    border: 2px solid black;
    border-radius: 50%;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
  }

  .volume-slider:disabled {
    opacity: 0.5;
    cursor: not-allowed;
  }

  .volume-text {
    font-size: clamp(9px, 2.2vw, 11px);
    color: var(--color-accent);
    min-width: clamp(35px, 10vw, 45px);
    font-family: 'Courier New', monospace;
    font-weight: bold;
    text-align: center;
  }

  .music-status {
    display: flex;
    align-items: center;
    gap: clamp(6px, 2vw, 8px);
    margin-left: auto;
    padding: clamp(4px, 2vw, 8px) clamp(8px, 3.5vw, 16px);
    background: rgba(134, 193, 252, 0.1);
    border: 1px solid rgba(134, 193, 252, 0.3);
    border-radius: 8px;
    flex-shrink: 0;
  }

  .status-indicator {
    width: clamp(10px, 3vw, 12px);
    height: clamp(10px, 3vw, 12px);
    background: var(--fg-light);
    border: 2px solid var(--fg-light);
    border-radius: 50%;
    transition: all 0.3s ease;
  }

  .status-indicator.active {
    background: #00ff41;
    border-color: #00ff41;
    box-shadow: 0 0 12px #00ff4180;
    animation: pulse 2s infinite;
  }

  @keyframes pulse {
    0%, 100% { 
      opacity: 1; 
      transform: scale(1);
    }
    50% { 
      opacity: 0.7; 
      transform: scale(1.1);
    }
  }

  .status-text {
    font-size: clamp(9px, 2.2vw, 11px);
    color: var(--color-accent);
    font-family: 'Courier New', monospace;
    letter-spacing: 1px;
    font-weight: bold;
  }

  .filler {
    height: clamp(3rem, 8vw, 3.5rem);
  }

  .retro-overlay {
    position: fixed;
    top: 0;
    left: 0;
    background: 
      repeating-linear-gradient(
        0deg,
        transparent 0px,
        transparent 2px,
        rgba(25, 50, 128, 0.15) 2px,
        rgba(25, 50, 128, 0.15) 3px,
        transparent 3px,
        transparent 8px
      ),
      radial-gradient(
        ellipse at center,
        rgba(25, 50, 128, 0.05) 0%,
        rgba(25, 50, 128, 0.08) 50%,
        rgba(10, 25, 64, 0.12) 100%
      );
    pointer-events: none;
    animation: tv-scanlines 40s infinite linear, tv-flicker 8s infinite ease-in-out;
    z-index: 999999999;
  }

  .retro-overlay.hidden-on-projects {
    display: none;
  }

  @keyframes tv-scanlines {
    0% { background-position: 0 0, center; }
    100% { background-position: 0 100px, center; }
  }

  @keyframes tv-flicker {
    0% { opacity: 1; filter: brightness(1) contrast(1.1); }
    15% { opacity: 0.98; filter: brightness(1.02) contrast(1.15); }
    30% { opacity: 1; filter: brightness(0.98) contrast(1.1); }
    60% { opacity: 0.99; filter: brightness(1.01) contrast(1.12); }
    85% { opacity: 1; filter: brightness(0.99) contrast(1.1); }
    100% { opacity: 1; filter: brightness(1) contrast(1.1); }
  }

  /* Responsive Breakpoints */
  @media screen and (max-width: 768px) {
    .desktop-nav {
      display: none;
    }

    .mobile-nav {
      display: flex;
    }
  }

  @media screen and (max-width: 480px) {
    .mobile-dropdown-nav {
      padding: 0.8rem;
    }

    .mobile-nav__link {
      font-size: 0.9rem;
      padding: 0.8rem 1.2rem;
    }

    .music-status {
      display: none;
    }

    .volume-control {
      min-width: 80px;
    }

    .music-controls {
      gap: 4px;
    }
  }

  @media screen and (max-width: 360px) {
    .logo-text {
      display: none;
    }

    .volume-control {
      min-width: 70px;
    }
  }

  @media screen and (max-width: 320px) {
    .music-toggle-btn {
      width: 25px;
      height: 25px;
      font-size: 10px;
    }

    .volume-control {
      min-width: 60px;
    }
  }
</style>