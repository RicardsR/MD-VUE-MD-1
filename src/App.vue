<template>
  <div id="app">
    <HeaderComponent @login="handleLogin" @logout="handleLogout" />
    <div v-if="isLoggedIn">
      <div class="container">
        <div>
          <NavigationComponent @change-component="changeComponent" :isHomeActive="isHomeActive"
            :isAboutMeActive="isAboutMeActive" />
        </div>
        <div>
          <HomeComponent v-if="currentComponent === 'home'" />
          <AboutMeComponent v-if="currentComponent === 'aboutMe'" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import HeaderComponent from "@/components/HeaderComponent.vue";
import NavigationComponent from "@/components/NavigationComponent.vue";
import HomeComponent from "@/components/HomeComponent.vue";
import AboutMeComponent from "@/components/AboutMeComponent.vue";

export default {
  data() {
    return {
      isLoggedIn: false,
      currentComponent: "home",
    };
  },
  components: {
    HeaderComponent,
    NavigationComponent,
    HomeComponent,
    AboutMeComponent,
  },
  methods: {
    handleLogin() {
      this.isLoggedIn = true;
    },
    handleLogout() {
      this.isLoggedIn = false;
    },
    changeComponent(componentName) {
      this.currentComponent = componentName;
      this.isHomeActive = componentName === "home";
      this.isAboutMeActive = componentName === "aboutMe";
    },
  },
};
</script>