<template>
  <div class="online-experiences">
    <div class="online-experiences__top">
      <div class="online-experiences__title-and-sub">
        <div
          class="online-experiences__title section-title section-title--white"
        >
          Online Experiences for the Holidays
        </div>
        <div class="online-experiences__sub">
          Interactive activities we can do together, led by one-of-a-kind hosts.
        </div>
      </div>
      <a href="javascript:;" class="button online-experiences__button online-experiences__button--large-screens-only"
        >Explore all</a
      >
    </div>
    <div class="online-experiences__bottom">
      <a
        v-for="(exp, index) in experiences"
        :key="index"
        href="javascript:;"
        class="image-card"
        :class="exp.eclass"
      >
        <img
          :src="require(`../assets/${exp.eimg}`)"
          :alt="exp.etext"
          class="image-card__image"
        />
        <div class="image-card__text">
          {{exp.etext}}
        </div>
      </a>
    </div>
    <a href="javascript:;" class="button online-experiences__button online-experiences__button--small-screens-only"
        >Explore all</a
      >
  </div>
</template>

<script>
export default {
  name: "OnlineExperiencesComponent",
  data() {
    return {
      experiences: [
        {
          etext: `Enjoy Santa stories with a children’s book author`,
          eimg: "santa.jpg",
          eclass: "online-experiences__grid-element--one",
        },
        {
          etext: "Discover spiced wines with an archaeologist",
          eimg: "garyvee.jpg",
          eclass: "online-experiences__grid-element--two",
        },
        {
          etext: "Sing Holiday songs with a Broadway star",
          eimg: "italian.jpg",
          eclass: "online-experiences__grid-element--three",
        },
        {
          etext: "Cook pasta at home with Italian grandmas",
          eimg: "grandma.jpg",
          eclass: "online-experiences__grid-element--four",
        },
      ],
    };
  },
};
</script>