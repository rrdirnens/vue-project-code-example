<template>
  <div class="inspirations">
    <div class="inspirations__title section-title section-title--black">
      Inspirations for future getaways
    </div>
    <div class="inspirations__tabs">
      <div class="inspirations__tab-controls">
        <a
          href="#tab-1"
          class="button inspirations__tab-controls-single inspirations__tab-controls-single--active"
        >
          Destinations for arts & culture
        </a>
        <a href="#tab-2" class="button inspirations__tab-controls-single">
          Destinations for outdoor adventure
        </a>
        <a href="#tab-3" class="button inspirations__tab-controls-single">
          Mountain cabins
        </a>
        <a href="#tab-4" class="button inspirations__tab-controls-single">
          Beach destinations
        </a>
        <a href="#tab-5" class="button inspirations__tab-controls-single">
          Popular destinations
        </a>
      </div>
      <div v-if="!citiesApi.loading && !citiesApi.errored" class="inspirations__tab-panes">
        <div
          id="tab-1"
          class="inspirations__tab-panes-single inspirations__tab-panes-single--active"
        >
          <ul class="inspirations__tab-values-list">
            <li
              v-for="(place, index) in groupArtsAndCulture"
              :key="index"
              class="inspirations__tab-values-single"
            >
              <a
                :href="place.flag"
                target="_blank"
                class="inspirations__tab-values-single-link"
              >
                <div class="inspirations__tab-values-single-top">
                  {{ place.name }}
                </div>
                <div class="inspirations__tab-values-single-bottom">
                  {{ place.capital }}
                </div>
              </a>
            </li>
          </ul>
        </div>
        <div id="tab-2" class="inspirations__tab-panes-single">
          <ul class="inspirations__tab-values-list">
            <li v-for="(place, index) in groupOutdoor" :key="index" class="inspirations__tab-values-single">
              <a
                :href="place.flag"
                class="inspirations__tab-values-single-link"
                target="_blank"
              >
                <div class="inspirations__tab-values-single-top">{{place.name}}</div>
                <div class="inspirations__tab-values-single-bottom">
                  {{place.capital}}
                </div>
              </a>
            </li>
            
          </ul>
        </div>
        <div id="tab-3" class="inspirations__tab-panes-single">
          <ul class="inspirations__tab-values-list">
            <li v-for="(place, index) in groupMountains" :key="index" class="inspirations__tab-values-single">
              <a
                :href="place.flag"
                class="inspirations__tab-values-single-link"
                target="_blank"
              >
                <div class="inspirations__tab-values-single-top">{{place.name}}</div>
                <div class="inspirations__tab-values-single-bottom">
                  {{place.capital}}
                </div>
              </a>
            </li>
          </ul>
        </div>
        <div id="tab-4" class="inspirations__tab-panes-single">
          <ul class="inspirations__tab-values-list">
            <li v-for="(place, index) in groupBeaches" :key="index" class="inspirations__tab-values-single">
              <a
                :href="place.flag"
                class="inspirations__tab-values-single-link"
                target="_blank"
              >
                <div class="inspirations__tab-values-single-top">{{place.name}}</div>
                <div class="inspirations__tab-values-single-bottom">
                  {{place.capital}}
                </div>
              </a>
            </li>
          </ul>
        </div>
        <div id="tab-5" class="inspirations__tab-panes-single">
          <ul class="inspirations__tab-values-list">
            <li v-for="(place, index) in groupPopular" :key="index" class="inspirations__tab-values-single">
              <a
                :href="place.flag"
                class="inspirations__tab-values-single-link"
                target="_blank"
              >
                <div class="inspirations__tab-values-single-top">{{place.name}}</div>
                <div class="inspirations__tab-values-single-bottom">
                  {{place.capital}}
                </div>
              </a>
            </li>
          </ul>
        </div>
      </div>
      <div v-if="citiesApi.errored" class="inspirations__error">
        Couldn't retrieve data from the API, try again later
      </div>
      <div v-if="citiesApi.loading" class="inspirations__loading">
        Still loading
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "InspirationsComponent",
  data() {
    return {
      apiInfo: null,
      groupArtsAndCulture: [],
      groupOutdoor: [],
      groupMountains: [],
      groupBeaches: [],
      groupPopular: [],
      citiesApi: {
        errored: false,
        loading: true,
        info: null,
      },
    };
  },

  mounted() {
    this.axios({
      method: "get",
      url: "https://restcountries.eu/rest/v2/all"
    })
      .then((response) => {
        this.citiesApi.info = response.data;
        let self = this;
        response.data.forEach((e, i) => {
          if (i <= 31) {
            self.groupArtsAndCulture.push(e);
          } else if (i >= 32 && i <= 63) {
            self.groupOutdoor.push(e);
          } else if (i >= 64 && i <= 95) {
            self.groupMountains.push(e);
          } else if (i >= 96 && i <= 127) {
            self.groupBeaches.push(e);
          } else if (i >= 128 && i <= 159) {
            self.groupPopular.push(e);
          }
        });
      })
      .catch((error) => {
        console.log(error);
        this.citiesApi.errored = true;
      })
      .finally(
        () => (this.citiesApi.loading = false)
      );
  },

  created() {
    window.addEventListener("load", function () {
      // store tabs variable
      var myTabs = document.querySelectorAll(
        ".inspirations__tab-controls-single"
      );

      function myTabClicks(tabClickEvent) {
        for (var i = 0; i < myTabs.length; i++) {
          myTabs[i].classList.remove(
            "inspirations__tab-controls-single--active"
          );
        }

        var clickedTab = tabClickEvent.currentTarget;

        clickedTab.classList.add("inspirations__tab-controls-single--active");

        tabClickEvent.preventDefault();

        var myContentPanes = document.querySelectorAll(
          ".inspirations__tab-panes-single"
        );

        for (i = 0; i < myContentPanes.length; i++) {
          myContentPanes[i].classList.remove(
            "inspirations__tab-panes-single--active"
          );
        }

        var anchorReference = tabClickEvent.target;
        var activePaneId = anchorReference.getAttribute("href");
        var activePane = document.querySelector(activePaneId);

        activePane.classList.add("inspirations__tab-panes-single--active");
      }

      for (let i = 0; i < myTabs.length; i++) {
        myTabs[i].addEventListener("click", myTabClicks);
      }
    });
  },
};
</script>