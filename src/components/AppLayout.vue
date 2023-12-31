<script setup>
import { computed } from "vue";
import { useRoute, useRouter } from "vue-router";

import { Back } from "@element-plus/icons-vue";
import { ROUTES_PATHS } from "@/constants";
const props = defineProps({
  imgUrl: {
    type: String,
    required: true,
  },
  backFunc: {
    type: Function,
  },
  isBackVisable: {
    type: Boolean,
    default: true,
  },
});

const route = useRoute();
const router = useRouter();
const routeName = computed(() => route.name);

function goToCocktailRandom() {
  router.push(ROUTES_PATHS.COCKTAIL_RANDOM);

  if (routeName.value === ROUTES_PATHS.COCKTAIL_RANDOM) {
    router.go();
  }
}

function goBack() {
  props.backFunc ? props.backFunc() : router.go(-1);
}
</script>

<template>
  <div class="root">
    <div :style="`background-image : url(${imgUrl})`" class="img"></div>
    <div class="main">
      <div class="btns">
        <el-button
          type="primary"
          circle
          :icon="Back"
          class="back"
          @click="goBack"
          v-if="isBackVisable"
        />
        <el-button class="btn" @click="goToCocktailRandom"
          >Get random cocktail</el-button
        >
      </div>

      <slot></slot>
    </div>
  </div>
</template>

<style lang="sass" scoped>
@import '../assets/styles/main'

.root
  display: flex
  min-height: 100vh
  background: $background

.img
  width: 50%
  background-repeat: no-repeat
  background-position: 50% 50%
  background-size: cover

.main
  width: 50%
  position: relative
  padding: 32px 40px

.btn
  position: absolute
  top: 32px
  right: 40px
  background-color: $accent
  border: $accent
  color: $text
  font-size: 16px
  line-height: 1.4
  font-family: "Railway", "Arial", sans-serif

  &:hover,
  &:active
    background-color: darken($accent, 10%)
    border: darken($accent, 10%)

.btns
  display: flex
  justify-content: space-between
  align-content: center

.back
  background-color: transparent
  border-color: #fff

  &:hover
    border-color: $accent
</style>