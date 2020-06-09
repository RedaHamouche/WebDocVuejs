<template>
  <div class="navBar">
    <div class="navBar__timeLineContainer">
      <div>
        <router-link to="/">
          <img src="../assets/logo/earth-logo.png" alt="earth-logo" class="navBar__earthLogo" />
        </router-link>
      </div>
      <div
        class="navBar__containerVolumeLogo"
        @click="toggleMute"
        :class="isMute ? 'isMute' : null"
      >
        <img src="../assets/logo/volume-logo.png" alt="volume-logo" class="navBar__volumeLogo" />
      </div>
      <nav class="navBar__timeLine">
        <div @click="jumpToOtherChapter(scroll * 5)" :class="page === 1 ? 'isSelected' : null">
          <p>The Journey</p>
        </div>
        <div @click="jumpToOtherChapter(scroll * 15)" :class="page === 2 ? 'isSelected' : null">
          <p>How to use it</p>
        </div>
        <div @click="jumpToOtherChapter(scroll * 25)" :class="page === 3 ? 'isSelected' : null">
          <p>Visual Content</p>
        </div>
        <div @click="jumpToOtherChapter(scroll * 35)" :class="page === 4 ? 'isSelected' : null">
          <p>Audio Content</p>
        </div>
        <div @click="jumpToOtherChapter(scroll * 45)" :class="page === 5 ? 'isSelected' : null">
          <p>Who did it ?</p>
        </div>
      </nav>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isMute: false
    };
  },
  methods: {
    toggleMute() {
      this.isMute = !this.isMute;
    },
    jumpToOtherChapter(value) {
      this.$emit("jumpToOtherChapter", value);
    }
  },
  props: {
    page: {
      type: Number
    },
    scroll: {
      type: Number
    }
  }
};
</script>

<style lang="scss" scoped>
.navBar__timeLineContainer {
  position: fixed;
  display: flex;
  align-items: center;
  top: 0;
  left: 0;
  height: 100vh;
  width: 60px;
  background-color: $primary-darkblue;
  transition: width 0.2s;
  overflow: hidden;

  &:hover {
    transform: none;
    width: 250px;

    & nav div {
      & p {
        clip-path: polygon(0 0, 100% 0, 100% 100%, 0% 100%);
        transform: none;
        opacity: 0.7;
        left: 10px;
        top: -10px;
        width: 150px;
      }
      &.isSelected p {
        font-size: 1.02rem;
        opacity: 1;
      }
    }
  }
}

@keyframes chapterTitleShowUp {
  to {
    clip-path: polygon(0 0, 100% 0, 100% 100%, 0% 100%);
  }
}

.navBar__timeLine {
  height: 70%;
  width: 2px;
  background-color: $primary-white;
  margin-left: 27px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;

  & div {
    position: relative;
    background-color: $primary-darkblue;
    left: -200%;
    width: 10px;
    height: 10px;
    border-radius: 50%;
    border: 2px solid $primary-white;
    &.isSelected {
      background-color: $primary-white;
      & p {
        animation: chapterTitleShowUp 1.5s forwards;
      }
    }

    & p {
      position: absolute;
      clip-path: polygon(0 0, 0 0, 0 99%, 0% 100%);
      left: -52px;
      top: -200%;
      transform: rotate(-90deg);
      color: $primary-white;
      font-weight: bold;
      font-size: 0.8rem;
      background-color: $primary-darkblue;
      padding: 5px 0;
      width: 110px;

      &:hover {
        cursor: pointer;
        text-decoration: underline;
      }
    }
  }
}

.navBar__earthLogo {
  z-index: 2;
  position: fixed;
  top: 15px;
  left: 15px;
  width: 30px;
  height: 30px;
  cursor: pointer;
  transition: transform 0.1s;

  &:hover {
    transform: scale(1.1);
  }
}

.navBar__containerVolumeLogo {
  position: fixed;
  z-index: 2;
  left: 17px;
  bottom: 15px;
  width: 20px;
  height: 20px;
  cursor: pointer;

  & img {
    width: 100%;
    height: 100%;
  }

  &:hover {
    transform: scale(1.1);
  }

  &.isMute::after {
    content: "";
    position: absolute;
    display: block;
    width: 30px;
    height: 2px;
    background-color: $primary-white;
    border: 0.2px solid $primary-darkblue;
    transform: translateY(-12px) translatex(-7px) rotate(-45deg);
  }
}
</style>