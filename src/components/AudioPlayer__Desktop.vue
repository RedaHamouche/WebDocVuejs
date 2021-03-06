<template>
  <div class="player">
    <audio ref="audio" autoplay @playing="isPlaying" @ended="isFinish">
      <source type="audio/mpeg" />
    </audio>
    <svg class="svgSettings" @click="togglePlay">
      <use :href="playing ? '#pause' : '#play'" />
    </svg>
    <svg class="svgSettings" @click="nextMusic">
      <use href="#next" />
    </svg>
    <div class="player__soundSettings">
      <svg @click="toggleMuted">
        <use :href="muted ? '#soundoff' : '#soundon'" />
      </svg>
      <input
        class="player__soundSlider"
        ref="slider"
        type="range"
        min="0"
        max="100"
        step="1"
        value="50"
        @input="updateVolume"
      />
    </div>
    <div class="player__titleContainer">
      <p class="player__title">{{ name }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "AudioPlayer",
  props: {
    source: {
      type: String,
      required: true,
    },
    name: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      playing: true,
      muted: false,
      volume: 0,
    };
  },
  computed: {
    audio() {
      return this.$refs["audio"];
    },
    slider() {
      return this.$refs["slider"];
    },
  },
  methods: {
    togglePlay() {
      if (!this.audio.paused && !this.audio.ended) {
        ///
        this.$emit("pause-event");
        ///
        this.audio.pause();
        this.playing = false;
      } else {
        this.audio.play();
        //
        this.$emit("play-event");
        //
        this.playing = true;
      }
    },
    updateVolume: function(e) {
      this.volume = e.target.value;
      this.audio.volume = this.volume / 100;
      this.volume == 0 ? (this.muted = true) : (this.muted = false);
    },
    toggleMuted() {
      this.muted = !this.muted;
      let volumeNow = this.audio.volume * 100;
      if (this.audio.muted != true) {
        this.audio.muted = true;
        this.slider.value = 0;
      } else {
        this.audio.muted = false;
        this.slider.value = volumeNow;
      }
    },
    nextMusic() {
      this.$emit("next-music");
    },
    isFinish() {
      this.$emit("pause-event");
      return (this.playing = false);
    },
    isPlaying() {
      return (this.playing = true);
    },
  },
  watch: {
    source: function(newProps) {
      this.audio.src = newProps;
    },
  },
};
</script>

<style lang="scss" scoped>
svg,
input {
  cursor: pointer;
}

.player {
  margin: 0 2vh 0 25vh;
  padding-top: 2vh;
  display: flex;
  justify-content: flex-start;
  align-items: center;
  transform: translateY(4vh);
  opacity: 0;
  transition: transform 1s, opacity 1s;

  &--isFocus {
    transform: translateY(-3vh);
    opacity: 1;

    @include media_mobile {
      transform: translateY(-1.5vh);
      height: 200px;
      flex-direction: column;
      justify-content: space-between;
      align-items: center;
      transform: translateY(-8.5vh);
    }
  }

  @include media_tablet {
    margin: 0 2vh 0 10vh;
  }
}

.svgSettings {
  width: 50px;
  height: 50px;

  &:nth-child(2) {
    margin: 0 3vh;
  }

  @include media_mobile {
    min-width: 25px;
    min-height: 25px;
  }
}

.player__titleContainer {
  padding: 0.5vh 0;
  overflow-x: hidden;
}

.player__title {
  width: 100%;
  display: inline-block;
  color: $primary-white;
  font-size: 1rem;
  user-select: none;
  text-align: initial;

  @include media_tablet {
    font-size: 0.8rem;
  }
}

.player__soundSettings {
  margin: 0 4vw 0 2vw;
  display: flex;
  align-items: center;

  svg {
    width: 24px;
    height: 24px;
    fill: #ae8908;
  }
}

.player__soundSettings input {
  -webkit-appearance: none; /* reset default style for chrome */
  -moz-appearance: none; /* reset default style for mozz */
  outline: none;
  background-color: transparent;
  margin-left: 16px;
}

/* slider for chrome*/
.player__soundSettings input::-webkit-slider-runnable-track {
  height: 4px;
  border: none;
  border-radius: 10px;
  background-color: $primary-white;
}

/* slider for mozz */
.player__soundSettings input::-moz-range-track {
  height: 4px;
  border: none;
  border-radius: 10px;
  background-color: $primary-white;
}

/* cursor for chrome*/
.player__soundSettings input::-webkit-slider-thumb {
  -webkit-appearance: none;
  width: 8px;
  height: 8px;
  border: 1px solid #ae8908;
  border-radius: 50%;
  padding: 4px;
  background: #ae8908;
  margin-top: -3px;
}

/* cursor for mozz */
.player__soundSettings input::-moz-range-thumb {
  -moz-appearance: none;
  width: 4px;
  height: 4px;
  border: none;
  border-radius: 50%;
  padding: 4px;
  background: #ae8908;
  margin-top: -3px;
}
</style>
