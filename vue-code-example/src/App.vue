<template>
  <HeaderComponent msg="airbnb clone"/>
</template>

<script>
import HeaderComponent from './components/HeaderComponent.vue'

export default {
  name: 'App',
  components: {
    HeaderComponent
  }
}
</script>

<style lang="scss">

@import './scss/app.scss';

</style>