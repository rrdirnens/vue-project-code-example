<template>
  <section class="hero-section">
    <div class="container">
      <HeaderComponent/>
      <HeroComponent/>
    </div>
  </section>
</template>

<script>
import HeaderComponent from "./components/HeaderComponent.vue";
import HeroComponent from "./components/HeroComponent.vue";

export default {
  name: "App",
  components: {
    HeaderComponent,
    HeroComponent
  },
};
</script>

<style lang="scss">
@import "./scss/app.scss";
</style>