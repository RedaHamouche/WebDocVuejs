<template>
  <div :index="index" @click="openModal" v-on="$listeners" class="Use__symbol">
    <slot name="left"></slot>
    <BaseIcon class="Use__svg" :href="nameIcon" />
    <slot name="right"></slot>
    <Icon />
  </div>
</template>

<script>
import EventBus from "@/EventBus";
import BaseIcon from "@/components/BaseIcon.vue";
import Icon from "@/components/Icons.vue";
import { url } from "@/constants.js";

export default {
  props: {
    nameIcon: {
      type: String,
      required: false
    },
    index: {
      type: Number,
      required: true,
      default: 0
    }
  },
  components: {
    BaseIcon,
    Icon
  },
  data: () => ({
    modalContent: {
      text1: "",
      text2: "",
      title: "",
      symbol: "nameIcon"
    }
  }),
  methods: {
    openModal() {
      EventBus.$emit("open", {
        component: "BaseModal",
        content: this.modalContent
      });
    }
  },
  created() {
    fetch(`${url}/query/how_use`, {
      method: "GET"
    })
      .then(Response => Response.json())
      .then(data => {
        this.modalContent = {
          text1: data[this.index].text_1,
          text2: data[this.index].text_2,
          title: data[this.index].title,
          symbol: data[this.index].symbol
        };
      })
      .catch(error => console.log(error));
  }
};
</script>

<style lang="scss">
.Use {
  &__symbol {
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
    // border: 1px solid red;
    height: 40%;
    opacity: 0.4;
    cursor: pointer;

    @include media_tablet {
      height: 40%;
    }

    &:hover {
      opacity: 1;
    }
  }

  &__title {
    font-family: Product Sans;
    font-size: 20px;
    color: $primary-white;

    @include media_tablet {
      font-size: 16px;
    }
  }

  &__plus {
    width: 20px;
    height: 20px;

    &--left {
      margin-left: 10px;
    }
  }

  &__svg {
    width: 140px;
    height: 120px;
    stroke: $primary-white;
    // border: 1px solid yellow;
    fill: none;

    @include media_tablet {
      width: 55%;
      height: 50%;
    }
  }
}
</style>
