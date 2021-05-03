<template>
  <v-app :style="{
    backgroundImage: `url(${require('@/assets/dragon1.png')})`,
    backgroundColor: `black`,
    backgroundRepeat: `no-repeat`,
    backgroundSize: `contain`
    }">
    <v-main :style="{
      minWidth: `Math.min(400px, windowWidth)`,
      maxWidth: `400px`,
      margin: `auto`
      }">
      <CookieRun/>
    </v-main>
  </v-app>
</template>

<script>
import CookieRun from './components/CookieRun';

export default {
  name: 'App',

  components: {
    CookieRun,
  },

  data: () => ({
    windowWidth: window.innerWidth
  }),
  mounted() {
      window.onresize = () => {
          this.windowWidth = window.innerWidth
      }
  }
};
</script>
