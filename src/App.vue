<template>
 <Navbar />
  <div class="container-box">
    <div class="left">
      <CountriesList :countries="countriesListReduced"> </CountriesList>
    </div>
    <div class="right">
      <CountryDetails></CountryDetails>
    </div>
    <router-view />
   </div>
</template>

<script>
import Navbar from "./components/Navbar.vue";
import CountriesList from './views/CountriesList.vue';
import CountryDetails from "./views/CountryDetails.vue";
import json from "./assets/countries.json";

export default {
  data() {
    return {
      countriesJson: json,
    };
  },
  computed: {
    countriesListReduced() {
      let id = 0;
      let urlRoute = "https://flagpedia.net/data/flags/icon/72x54/";
      return this.countriesJson.map((countries) => {
        return {
          countryId: id++,
          countryName: countries.name.official,
          countryAlpha2Code: countries.alpha2Code.toLowerCase(),
          countryAlpha3Code: countries.alpha3Code,
          countryImageURL:
            urlRoute + countries.alpha2Code.toLowerCase() + ".png",
        };
      });
    },
  },
  components: { Navbar, CountriesList, CountryDetails },
};
</script>

<style scoped>
.container-box {
  display: flex;
  flex-direction: row;
  width: 100%;
}
.left {
  width: 40%;
  height: 100%;
  text-align: center,
}
.right {
  width: 60%;
   height: 100%;
  text-align: center,
}

</style>
