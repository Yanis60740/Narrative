<template>
  <LoadingScreen/>
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
import LoadingScreen from './components/LoadingScreen.vue'
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
    LoadingScreen,
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

@media screen and (max-width: 1200px) {
  .titleContainer__title{
    font-size: 84px !important;
  }

  .sentence{
    font-size: 32px !important;
  }

  .capabilitiesOverview__left p{
    font-size: 10px !important;
  }

  .capabilitiesOverview__right__intro p{
    font-size: 16px !important;
  }
  
  .featuredWorks__title p{
    font-size: 10px !important;
  }

  .animFeature__title{
    font-size: 51px !important;
  }

  .animFeature__animation__title€
  {
    font-size: 16px !important;
  }

  .craftsSection__title p{
    font-size: 10px !important;
  }

  .animFeature__animation__box{
    display: none;
  }

  .animFeature{
    padding: 32px !important;
    height: min-content !important;
  }

  .animMenu{
    font-size: 38px !important;
  }

  .navmenu__rightContent__link__title{
    font-size: 10px !important;
  }

  .navmenu__rightContent__link__content{
    font-size: 12px !important;
  }

  .navmenu__rightContent{
    gap: 20px !important;
  }
  
}

@media screen and (max-width: 900px) {
.nav{
  padding: 0 16px !important;
}

.titleContainer{
  padding: 5px 16px 80px !important;
  gap: 24px !important;
}
  .titleContainer__title{
    font-size: 54px !important;
  }

  .titleContainer__subtitle{
    flex-direction: column !important;
    align-items: flex-start !important;
  }

  .titleContainer__subtitle__left{
    flex: none !important;
    flex-direction: column;
  }
  .titleContainer__subtitle__right{
    flex: none !important;
  }

  .videoContainer{
    height: 364px !important;
    padding: 0 16px !important;
  }

  .aboutUs{
    padding: 80px 16px 0 !important;
  }

  .sentence{
    font-size: 24px !important;
  }

  .capabilitiesOverview{
    flex-direction: column !important;
    gap: 24px !important;
    padding: 80px 16px 0 !important;
  }

  .capabilitiesOverview__left{
    overflow: visible !important;
  }
  .capabilitiesOverview__left p{
    font-size: 10px !important;
  }

  .capabilitiesOverview__right__intro p{
    font-size: 16px !important;
  }
  
  .featuredWorks{
    padding: 64px 16px !important;
    gap: 32px !important;
  }

  .featuredWorks__title p{
    font-size: 10px !important;
  }

  .animFeature{
    padding: 32px 0 !important;
    height: min-content !important;
  }

  .animFeature__title{
    font-size: 28px !important;
  }

  .animFeature__animation
  {
    display: none !important;
  }

  .craftsSection{
    padding: 80px 16px !important;
  }

  .craftsSection__title p{
    font-size: 10px !important;
  }

  .footerNarrative{
    padding: 32px 32px 48px 16px !important;
  }

  .footerNarrative__content__info{
    flex-direction: column !important;
  }

  .footerNarrative__content__info__right{
    flex-direction: column !important;
    gap: 40px !important;
  }

  .footerNarrative__content__credits{
    flex-direction: column;
    gap: 20px !important;
  }

  .animFeature__animation__box{
    display: none;
  }

  

  .animMenu{
    font-size: 38px !important;
  }

  .navmenu__rightContent__link__title{
    font-size: 10px !important;
  }

  .navmenu__rightContent__link__content{
    font-size: 12px !important;
  }

  .navmenu__rightContent{
    gap: 20px !important;
  }
  
}
</style>
