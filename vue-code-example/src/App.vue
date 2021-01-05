<template>
  <section class="hero-section">
    <div class="container">
      <HeaderComponent/>
      <HeroComponent/>
    </div>
  </section>
  <section class="cities-section">
    <div class="container">
      <CitiesComponent/>
    </div>
  </section>
  <section class="home-categories-section">
    <div class="container">
      <HomeCategoriesComponent/>
    </div>
  </section>
  <section class="online-experiences-section">
    <div class="container">
      <OnlineExperiencesComponent/>
    </div>
  </section>
</template>

<script>
import HeaderComponent from "./components/HeaderComponent.vue";
import HeroComponent from "./components/HeroComponent.vue";
import CitiesComponent from "./components/CitiesComponent.vue";
import HomeCategoriesComponent from "./components/HomeCategoriesComponent.vue";
import OnlineExperiencesComponent from "./components/OnlineExperiencesComponent.vue";

export default {
  name: "App",
  components: {
    HeaderComponent,
    HeroComponent, 
    CitiesComponent,
    HomeCategoriesComponent,
    OnlineExperiencesComponent
  },
};
</script>

<style lang="scss">
@import "./scss/app.scss";
</style>