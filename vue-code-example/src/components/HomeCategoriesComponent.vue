<template>
  <div class="home-categories">
    <div class="home-categories__title section-title section-title--black">
      Live Anywhere
    </div>
    <div class="home-categories__list">
      <a v-for="(cat, index) in categories" :key="index" href="javascript:;" class="home-categories__single">
        <img
            :src="require( `../assets/${cat.cimg}`)"
            :alt="cat.cname"
            class="home-categories__single-image"
        />
        <div class="home-categories__single-name">{{cat.cname}}</div>
      </a>

    </div>
  </div>
</template>

<script>
export default {
  name: "HomeCategoriesComponent",
  data() {
    return {
      categories: [
          { cname: "Entire homes", cimg: "entire homes.jpg" },
          { cname: "Cabins & cottages", cimg: "cabins and cottages.jpg" },
          { cname: "Unique stays", cimg: "unique stays.jpg" },
          { cname: "Pets welcome", cimg: "pets welcome.jpg" }
      ],
    };
  },
};
</script>