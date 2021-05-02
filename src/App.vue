<template>
  <v-app :style="{
    backgroundImage: `url(${require('@/assets/dragon1.png')})`,
    backgroundColor: `black`,
    backgroundRepeat: `no-repeat`,
    backgroundSize: `contain`
    }">
    <v-main>
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
    //
  }),
};
</script>
