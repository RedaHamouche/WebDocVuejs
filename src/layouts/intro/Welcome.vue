<template>
  <div class="intro" @click="$emit('clickWelcome')">
    <div class="stars"></div>
    <div class="twinkling"></div>
    <div class="explaination" @click="closeOverlay" :class="{ close: overlayClicked }">
      <h2 class="explaination__title">Hi Stranger ! 👋🏼👽</h2>
      <p>Switch to deskop for a better experience</p>
      <p class="text-welcome">Click anywhere to continue</p>
    </div>

    <div class="infos__container">
      <h1 class="title-blur">
        <em>T</em>
        <em>h</em>
        <em>e</em>
        <em></em>
        <em>G</em>
        <em>o</em>
        <em>l</em>
        <em>d</em>
        <em>e</em>
        <em>n</em>
        <em></em>
        <em>R</em>
        <em>e</em>
        <em>c</em>
        <em>o</em>
        <em>r</em>
        <em>d</em>
      </h1>
      <h1 class="title-welcome">The Golden Record</h1>
      <p class="text-welcome">Click anywhere to start the documentary</p>
      <div class="icone-scroll__mobile">
        <svg
          width="15"
          height="18"
          viewBox="0 0 15 18"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M14.2003 8.79995C13.3003 7.84995 12.1003 7.19995 10.8503 6.94995C10.3003 6.79995 9.75028 6.69995 9.20028 6.64995C10.6003 4.99995 10.3503 2.49995 8.70028 1.09995C7.05028 -0.300053 4.55028 -0.0500529 3.15028 1.59995C1.75028 3.24995 2.00028 5.74995 3.65028 7.14995C3.95028 7.39995 4.25028 7.59995 4.55028 7.69995V8.79995L3.75028 8.04995C3.05028 7.34995 1.90028 7.34995 1.15028 8.04995C0.450279 8.74995 0.400278 9.84995 1.10028 10.5499L3.40028 13.2499C3.50028 13.9499 3.75028 14.5999 4.10028 15.1999C4.35028 15.6499 4.70028 16.0999 5.05028 16.4499V17.3999C5.05028 17.6999 5.25028 17.8999 5.55028 17.8999H12.3503C12.6003 17.8999 12.8503 17.6499 12.8503 17.3999V16.0999C13.8003 14.9499 14.3003 13.4999 14.3003 12.0499V9.14995C14.3503 8.94995 14.3003 8.84995 14.2003 8.79995V8.79995ZM3.20028 4.09995C3.20028 2.44995 4.55028 1.14995 6.20028 1.19995C7.85028 1.19995 9.15028 2.54995 9.10028 4.19995C9.10028 5.09995 8.70028 5.89995 8.00028 6.44995V3.94995C7.97475 3.51663 7.78443 3.1095 7.46834 2.812C7.15225 2.51451 6.73434 2.3492 6.30028 2.34995C5.40028 2.29995 4.60028 3.04995 4.60028 3.94995V6.54995C3.75028 6.04995 3.25028 5.09995 3.20028 4.09995ZM13.3503 11.9999C13.4003 13.2999 12.9503 14.5499 12.1003 15.5499C12.0003 15.6499 11.9003 15.7499 11.9003 15.8999V16.9499H6.10028V16.2499C6.10028 16.0999 6.00028 15.9499 5.90028 15.8499C5.55028 15.5499 5.25028 15.1999 5.00028 14.7499C4.70028 14.2499 4.50028 13.6499 4.40028 13.0499C4.40028 12.9499 4.35028 12.8499 4.30028 12.7499L1.90028 9.89995C1.75028 9.74995 1.65028 9.54995 1.65028 9.29995C1.65028 9.09995 1.75028 8.84995 1.90028 8.69995C2.25028 8.39995 2.75028 8.39995 3.10028 8.69995L4.55028 10.1499V11.6499L5.50028 11.1499V3.94995C5.55028 3.59995 5.85028 3.29995 6.25028 3.34995C6.60028 3.34995 6.95028 3.59995 6.95028 3.94995V9.69995L7.95028 9.89995V7.59995C8.00028 7.54995 8.05028 7.54995 8.10028 7.49995C8.45028 7.49995 8.80028 7.54995 9.15028 7.59995V10.1499L9.95028 10.2999V7.69995L10.5503 7.84995C10.8003 7.89995 11.0503 7.99995 11.3003 8.09995V10.5999L12.1003 10.7499V8.44995C12.5503 8.64995 12.9503 8.94995 13.3003 9.29995L13.3503 11.9999V11.9999Z"
            fill="white"
          />
        </svg>
      </div>
    </div>
    <div class="earth-bg-container">
      <img class="earth-bg" src="@/assets/earth-welcome.png" alt />
      <img class="song-bg" src="@/assets/golden-welcome.png" alt />
    </div>
  </div>
</template>

<script>
export default {
  name: "Welcome",
  data() {
    return {
      overlayClicked: false
    };
  },
  methods: {
    closeOverlay() {
      this.overlayClicked = true;
      this.$emit("closeOverlay");
    }
  }
};
</script>

<style lang="scss" scoped>
.text-welcome {
  cursor: pointer;
  user-select: none;
}
// Overlay
@media screen and(max-width: 768px) {
  .explaination {
    transition: opacity 0.2s ease;
    z-index: 100;
    width: 100vw;
    height: 100vh;
    background: rgba($color: #000000, $alpha: 0.95);
    position: absolute;
    display: flex;
    justify-content: space-around;
    align-items: center;
    flex-direction: column;
    padding: 100px 20vw;
    h2 {
      font-size: 30px;
    }
  }
}
@media screen and(min-width: 768px) {
  .explaination {
    display: none;
  }
}
.close {
  display: none;
}
</style>