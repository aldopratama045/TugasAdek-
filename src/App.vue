<template>
  <div id="app" class="app-container">
    <!-- Header dengan Tema Kemerdekaan yang Ditingkatkan -->
    <header class="header">
      <div class="flag-animation">
        <div class="stripe red-stripe"></div>
        <div class="stripe white-stripe"></div>
      </div>
      <div class="title-container">
        <h1 class="main-title">Dirgahayu Indonesia</h1>
        <div class="year-badge">2024</div>
      </div>
      <p class="subtitle">Merah Putih Mengalun dalam Irama Nasionalisme</p>
    </header>

    <!-- Dropdown yang Ditingkatkan -->
    <div class="song-selector">
      <label for="songSelect">Pilih Lagu Perjuangan:</label>
      <select id="songSelect" v-model="selectedSong" @change="updateAudioSrc">
        <option value="/audio/Indonesia-Raya.mp3">Indonesia Raya</option>
        <option value="/audio/IndonesiaPusaka.mp3">Indonesia Pusaka</option>
        <option value="/audio/MAJUTAKGENTAR.mp3">Maju Tak Gentar</option>
      </select>
    </div>

    <!-- Pemutar Audio dengan Visualisasi -->
    <div class="audio-player">
      <audio ref="audioPlayer" :src="audioSrc" @ended="onTrackEnd"></audio>
      <div class="audio-visualization" v-if="isPlaying">
        <div class="bar" v-for="n in 5" :key="n"></div>
      </div>
    </div>

    <!-- Kontrol Musik yang Ditingkatkan -->
    <div class="controls">
      <button class="control-btn" @click="togglePlayPause">
        <span class="btn-icon">{{ isPlaying ? '⏸' : '▶' }}</span>
        <span class="btn-text">{{ isPlaying ? 'Jeda' : 'Mainkan' }}</span>
      </button>
      <button class="control-btn stop-btn" @click="stopAudio">
        <span class="btn-icon">⏹</span>
        <span class="btn-text">Berhenti</span>
      </button>
    </div>

    <!-- Dekorasi yang Ditingkatkan -->
    <div class="decorations">
      <div class="garuda-container">
        <div class="garuda-silhouette"></div>
      </div>
      <div class="ornaments">
        <div class="batik-pattern left"></div>
        <div class="batik-pattern right"></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      selectedSong: "/audio/Indonesia-Raya.mp3",
      audioSrc: "/audio/Indonesia-Raya.mp3",
      isPlaying: false,
    };
  },
  methods: {
    togglePlayPause() {
      const audio = this.$refs.audioPlayer;
      if (this.isPlaying) {
        audio.pause();
      } else {
        audio.play();
      }
      this.isPlaying = !this.isPlaying;
    },
    stopAudio() {
      const audio = this.$refs.audioPlayer;
      audio.pause();
      audio.currentTime = 0;
      this.isPlaying = false;
    },
    updateAudioSrc() {
      this.audioSrc = this.selectedSong;
      this.stopAudio();
    },
    onTrackEnd() {
      this.isPlaying = false;
    },
  },
};
</script>

<style scoped>
/* Gaya Dasar yang Ditingkatkan */
.app-container {
  min-height: 100vh;
  background: linear-gradient(135deg, #f5f5f5 0%, #e0e0e0 100%);
  padding: 2rem;
  position: relative;
  overflow: hidden;
}

/* Header yang Ditingkatkan */
.header {
  position: relative;
  padding: 2rem;
  margin-bottom: 3rem;
}

.flag-animation {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 200px;
  overflow: hidden;
}

.stripe {
  height: 50%;
  width: 100%;
  position: relative;
}

.red-stripe {
  background: #FF0000;
  animation: waveRed 3s ease-in-out infinite;
}

.white-stripe {
  background: #FFFFFF;
  animation: waveWhite 3s ease-in-out infinite;
}

@keyframes waveRed {
  0%, 100% { transform: skewY(0deg); }
  50% { transform: skewY(2deg); }
}

@keyframes waveWhite {
  0%, 100% { transform: skewY(0deg); }
  50% { transform: skewY(-2deg); }
}

.title-container {
  position: relative;
  z-index: 2;
  margin-top: 220px;
}

.main-title {
  font-size: 3.5rem;
  font-weight: 800;
  color: #FF0000;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
  margin: 0;
  letter-spacing: 2px;
}

.year-badge {
  background: #FF0000;
  color: white;
  padding: 0.5rem 1.5rem;
  border-radius: 25px;
  display: inline-block;
  margin-top: 1rem;
  font-weight: bold;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.subtitle {
  font-size: 1.2rem;
  color: #666;
  margin-top: 1rem;
  font-style: italic;
}

/* Selector Lagu yang Ditingkatkan */
.song-selector {
  background: rgba(255, 255, 255, 0.9);
  padding: 1.5rem;
  border-radius: 15px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  margin-bottom: 2rem;
}

.song-selector select {
  background: #FF0000;
  color: white;
  padding: 0.8rem 1.5rem;
  border: none;
  border-radius: 10px;
  font-size: 1rem;
  cursor: pointer;
  transition: transform 0.3s ease;
}

.song-selector select:hover {
  transform: scale(1.02);
}

/* Audio Player yang Ditingkatkan */
.audio-player {
  margin: 2rem 0;
}

.audio-visualization {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 5px;
  height: 50px;
}

.bar {
  width: 4px;
  background: #FF0000;
  height: 20px;
  animation: soundBars 1s ease-in-out infinite;
}

.bar:nth-child(2) { animation-delay: 0.2s; }
.bar:nth-child(3) { animation-delay: 0.4s; }
.bar:nth-child(4) { animation-delay: 0.6s; }
.bar:nth-child(5) { animation-delay: 0.8s; }

@keyframes soundBars {
  0%, 100% { height: 20px; }
  50% { height: 40px; }
}

/* Kontrol yang Ditingkatkan */
.controls {
  display: flex;
  gap: 1rem;
  justify-content: center;
  margin: 2rem 0;
}

.control-btn {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 1rem 2rem;
  border: none;
  border-radius: 25px;
  background: #FF0000;
  color: white;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.control-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 8px rgba(0, 0, 0, 0.2);
}

.stop-btn {
  background: dark;
}

.btn-icon {
  font-size: 1.2rem;
}

/* Dekorasi yang Ditingkatkan */
.decorations {
  position: relative;
  margin-top: 3rem;
}

.garuda-container {
  width: 200px;
  height: 200px;
  margin: 0 auto;
  position: relative;
}

.garuda-silhouette {
  width: 100%;
  height: 100%;
  background: url('/images/garuda-silhouette.png') no-repeat center;
  background-size: contain;
  opacity: 0.2;
  animation: float 4s ease-in-out infinite;
}

.batik-pattern {
  position: absolute;
  width: 150px;
  height: 300px;
  background: url('/images/batik-pattern.png') repeat;
  opacity: 0.1;
}

.batik-pattern.left {
  left: 0;
  transform: rotate(-30deg);
}

.batik-pattern.right {
  right: 0;
  transform: rotate(30deg);
}

@keyframes float {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-20px); }
}

/* Responsive Design */
@media (max-width: 768px) {
  .main-title {
    font-size: 2.5rem;
  }
  
  .controls {
    flex-direction: column;
    align-items: center;
  }
  
  .control-btn {
    width: 100%;
    justify-content: center;
  }
}
</style>