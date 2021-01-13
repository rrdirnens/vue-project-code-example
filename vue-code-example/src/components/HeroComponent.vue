<template>
<div class="hero">
  <div class="hero__left">
    <div class="hero__title">Go <br>Near</div>
    <a href="javascript:;" class="button hero__button">Explore nearby stays</a>
  </div>
  <div class="hero__right">
    <QuizComponent/>
  </div>
</div>
</template>

<script>
import QuizComponent from "./QuizComponent.vue";

export default {
  name: "HeroComponent",
  components: {
    QuizComponent
  },
  data() {
    return {};
  },
};
</script>


