<template>
  <div class="cities">
    <a v-for="(city, index) in cities" :key="index" href="javascript:;" class="cities__single">
      <img
        :src="require( `../assets/${city.img}`)"
        alt="City image"
        class="cities__image"
      />
      <div class="cities__card-body">
        <div class="cities__name">{{city.cname}}</div>
        <div class="cities__drive-time">{{city.cdrivetime}} drive</div>
      </div>
    </a>
  </div>
</template>

<script>
export default {
  name: "CitiesComponent",
  data() {
    return {
        cities: [
            {cname: "Riga", cdrivetime: "3.5 hour", img: "birds.jpg"},
            {cname: "Liepaja", cdrivetime: "15 minute", img: "daytime-birds.jpg"},
            {cname: "Jurmala", cdrivetime: "1 hour", img: "daytime-moon.jpg"},
            {cname: "Ventspils", cdrivetime: "2 hour", img: "dusk-moon.jpg"},
            {cname: "Cesis", cdrivetime: "25 minute", img: "kite.jpg"},
            {cname: "Sigulda", cdrivetime: "45 minute", img: "moon.jpg"},
            {cname: "Kuldiga", cdrivetime: "50 minute", img: "nighttime-moon.jpg"},
            {cname: "Daugavpils", cdrivetime: "5 light year", img: "sky-rift.jpg"}
        ]
    };
  },
};
</script>