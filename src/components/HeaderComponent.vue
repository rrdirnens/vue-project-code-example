<template>
  <div class="header header--sticky">
    <div class="header__left">
      <a href="/">
        <img
        src="../../src/assets/logo.png"
        alt="Company logo"
        class="header__logo"
      />
      </a>
    </div>
    <div class="header__center">
      <a href="javascript:;" class="link header__link">Places to stay</a>
      <a href="javascript:;" class="link header__link">Experiences</a>
      <a href="javascript:;" class="link header__link">Online Experiences</a>
    </div>
    <div class="header__right">
      <a
        href="javascript:;"
        class="button header__button header__button--large-screens-only"
        >Become a host</a
      >

      <button class="header__account-hamburger">
        <div
          :class="{ 'hamburger-toggle--open': hamburger }"
          class="hamburger-toggle hamburger-toggle--header"
        >
          <div class="hamburger-toggle__line"></div>
          <div class="hamburger-toggle__line"></div>
          <div class="hamburger-toggle__line"></div>
        </div>
        <svg
          class="header__account-user-icon header__account-user-icon--large-screen-only"
          viewBox="0 0 32 32"
          xmlns="http://www.w3.org/2000/svg"
          aria-hidden="true"
          role="presentation"
          focusable="false"
        >
          <path
            d="m16 .7c-8.437 0-15.3 6.863-15.3 15.3s6.863 15.3 15.3 15.3 15.3-6.863 15.3-15.3-6.863-15.3-15.3-15.3zm0 28c-4.021 0-7.605-1.884-9.933-4.81a12.425 12.425 0 0 1 6.451-4.4 6.507 6.507 0 0 1 -3.018-5.49c0-3.584 2.916-6.5 6.5-6.5s6.5 2.916 6.5 6.5a6.513 6.513 0 0 1 -3.019 5.491 12.42 12.42 0 0 1 6.452 4.4c-2.328 2.925-5.912 4.809-9.933 4.809z"
          ></path>
        </svg>
      </button>
      <div v-if="hamburger" class="header__user-panel">
        <a
          href="javascript:;"
          class="header__user-panel-link header__user-panel-link--small-screen-only"
          >Places to stay</a
        >
        <a
          href="javascript:;"
          class="header__user-panel-link header__user-panel-link--small-screen-only"
          >Experiences</a
        >
        <a
          href="javascript:;"
          class="header__user-panel-link header__user-panel-link--small-screen-only"
          >Online-experiences</a
        >
        <a
          href="javascript:;"
          class="header__user-panel-link header__user-panel-link--large-screen-only"
          >Log in</a
        >
        <a
          href="javascript:;"
          class="header__user-panel-link header__user-panel-link--large-screen-only"
          >Sign up</a
        >
        <div class="header__user-panel-divider"></div>
        <a
          href="javascript:;"
          class="header__user-panel-link header__user-panel-link--large-screen-only"
          >Host your home</a
        >
        <a
          href="javascript:;"
          class="header__user-panel-link header__user-panel-link--large-screen-only"
          >Host your experience</a
        >
        <a
          href="javascript:;"
          class="header__user-panel-link header__user-panel-link--small-screen-only"
          >User dashboard</a
        >
        <a
          href="javascript:;"
          class="header__user-panel-link header__user-panel-link--small-screen-only"
          >Become a host</a
        >
        <a href="javascript:;" class="header__user-panel-link">Help</a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HeaderComponent",
  data() {
    return {
      hamburger: false,
    };
  },

  methods: {
    stickyHeader() {
      let navbar = document.querySelector(".header--sticky");
      let sticky = navbar.offsetTop;
      if (window.pageYOffset >= 160) {
        navbar.classList.add("header--sticky-on");
      } else {
        navbar.classList.remove("header--sticky-on");
      }
    },
  },

  created() {
    let self = this;
    document.addEventListener(
      "click",
      function (event) {
        if (self.hamburger === true) {
          if (
            event.target.matches(".header__account-hamburger") ||
            !event.target.closest(".header__user-panel")
          ) {
            self.hamburger = false;
          }
        } else if (self.hamburger == false) {
          if (event.target.matches(".header__account-hamburger")) {
              self.hamburger = true;
          }
        }
      },
      false
    );

    window.onscroll = function () {
      self.stickyHeader();
    };
  },
};
</script>


