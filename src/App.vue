<template>
  <NavBar/>
  <HeroBanner/>
  <AboutUs/>
  <CapabilitiesOverview/>
  <FeaturedWorks/>
  <CraftsSection/>
  <FooterNarrative/>
  <FixedButton/>
</template>

<script>
import NavBar from './components/NavBar.vue'
import HeroBanner from './components/HeroBanner.vue'
import AboutUs from './components/AboutUs.vue'
import CapabilitiesOverview from './components/CapabilitiesOverview.vue'
import FeaturedWorks from './components/FeaturedWorks.vue';
import CraftsSection from './components/CraftsSection.vue';
import FooterNarrative from './components/FooterNarrative.vue';
import FixedButton from './components/FixedButton.vue';

export default {
  name: 'App',
  components: {
    NavBar,
    HeroBanner,
    AboutUs,
    CapabilitiesOverview,
    FeaturedWorks,
    CraftsSection,
    FooterNarrative,
    FixedButton,
  },
  provide() {
    return {
      toggleTheme: this.toggleTheme,
      currentTheme: this.currentTheme
    };
  },
  data() {
    return {
      currentTheme: 'light'
    };
  },
  methods: {
    toggleTheme() {
      this.currentTheme = this.currentTheme === 'dark' ? 'light' : 'dark';
      document.documentElement.setAttribute('data-theme', this.currentTheme);
    }
  },
  mounted() {
    document.documentElement.setAttribute('data-theme', this.currentTheme);
  }
}
</script>

<style lang="scss" >
@import "css/global.scss";
</style>
