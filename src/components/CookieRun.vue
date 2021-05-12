<template>
  <v-container>
    <h1 class="pb-10">
      Cookie Run: Kingdom | Guild Battle | Red Velvet Dragon HP
    </h1>

    <h3>
      Dragon Level
    </h3>
    <v-slider
      v-model="slider_lv"
      thumb-label="always"
      color="red"
      :min="minLv"
      :max="maxLv"
    >
      <template v-slot:prepend>
        <v-icon
          @click="slider_lv--"
        >
          mdi-minus
        </v-icon>
      </template>

      <template v-slot:append>
        <v-icon
          @click="slider_lv++"
        >
          mdi-plus
        </v-icon>
      </template>
    </v-slider>

    <h3>
      Dragon HP(%)
    </h3>
    <v-slider
      v-model="slider_hp"
      thumb-label="always"
      color="red"
      :min="minHP"
      :max="maxHP"
    >   
      <template v-slot:prepend>
        <v-icon
          @click="slider_hp--"
        >
          mdi-minus
        </v-icon>
      </template>

      <template v-slot:append>
        <v-icon
          @click="slider_hp++"
        >
          mdi-plus
        </v-icon>
      </template>
    </v-slider>

    <h3>
      Full HP
    </h3>
    <v-btn
      text
      icon
      outlined
      id="copyBtn"
      class="mr-3"
      @click.stop.prevent="copyTxt"
    >
      <v-icon small>mdi-content-copy</v-icon>
    </v-btn>
    <p class="pl-2 pb-4">
      Lv.{{slider_lv}}<br/>
      {{dragonHP[slider_lv].toLocaleString()}}<br/>
      {{calTxt(dragonHP[slider_lv] / 10000)}}
    </p>
    <input type="hidden" :value="fullHPTxt()">

    <h3>
      Left HP
    </h3>
    <v-btn
      text
      icon
      outlined
      id="copyBtn"
      class="mr-3"
      @click.stop.prevent="copyTxt"
    >
      <v-icon small>mdi-content-copy</v-icon>
    </v-btn>
    <p class="pl-2 pb-4" @click.stop.prevent="copyTxt">
      Lv.{{slider_lv}} | {{slider_hp}}%<br/>
      {{calMinHP().toLocaleString()}} ~ {{calMaxHP().toLocaleString()}}<br/>
      {{calTxt(calMinHP() / 10000)}} ~ {{calTxt(calMaxHP() / 10000)}}
    </p>
    <input type="hidden" :value="leftHPTxt()">

    <v-expand-transition>
      <v-alert v-show="alertSuccess"
      dense
      outlined
      type="success"
      >copied!</v-alert>
    </v-expand-transition>
    <v-expand-transition>
      <v-alert v-show="alertFail"
      dense
      outlined
      type="error"
      >unable to copy</v-alert>
    </v-expand-transition>
  </v-container>
</template>

<script>
  export default {
    name: 'CookieRun',

    data: () => ({
      alertSuccess: false,
      alertFail: false,
      minLv: 1,
      maxLv: 60,
      minHP: 1,
      maxHP: 99,
      slider_lv: 20,
      slider_hp: 50,
      dragonHP: [
        0,
        3000000,
        3150000,
        3474000,
        3648000,
        3830000,
        4022000,
        4224000,
        4436000,
        4658000,
        4890000,
        5134000,
        5390000,
        5660000,
        5944000,
        6242000,
        6554000,
        6882000,
        7226000,
        7588000,
        8366000,
        9224000,
        10170000,
        11212000,
        12360000,
        13626000,
        15024000,
        16564000,
        18262000,
        20134000,
        22198000,
        24474000,
        26982000,
        29748000,
        32798000,
        35472000,
        37632000,
        39922000,
        42354000,
        44932000,
        47206000,
        49114000,
        50980000,
        53162000,
        55310000,
        57262000,
        58992000,
        60774000,
        62612000,
        64506000,
        66456000,
        68464000,
        70532000,
        72664000,
        74860000,
        77122000,
        79452000,
        81854000,
        84328000,
        86876000,
        89502000,
        ],
    }),
    methods: {
      setCookieLv() {
        this.$cookies.set("cookieLv", this.slider_lv);
      },
      setCookieHp() {
        this.$cookies.set("cookieHp", this.slider_hp);
      },
      calMinHP() {
        return this.dragonHP[this.slider_lv] * this.slider_hp / 100;
      },
      calMaxHP() {
        return this.dragonHP[this.slider_lv] * (this.slider_hp + 1) / 100 - 1;
      },
      calTxt(value) {
        return Math.floor(value) + "만";
      },
      fullHPTxt() {
        return "Lv." + this.slider_lv + " | Full HP: " + this.calTxt(this.dragonHP[this.slider_lv] / 10000);
      },
      leftHPTxt() {
        return "Lv." + this.slider_lv + " | " + this.slider_hp + "% Left HP: " + this.calTxt(this.calMinHP() / 10000) + " ~ " + this.calTxt(this.calMaxHP() / 10000);
      },
      copyTxt(event) {
        let target = event.currentTarget.nextSibling.nextSibling;

        target.setAttribute('type', 'text');
        target.select();

        try {
          document.execCommand('copy');
          this.alertSuccess = true;
          setTimeout(() => { this.alertSuccess = false }, 1000);
        } catch (err) {
          this.alertFail = true;
          setTimeout(() => { this.alertFail = false }, 1000);
        }

        /* unselect the range */
        target.setAttribute('type', 'hidden');
        window.getSelection().removeAllRanges();
      },
    },
    created() {
      if (this.$cookies.isKey("cookieLv")) {
        this.slider_lv = this.$cookies.get("cookieLv");
      }
      
      if (this.$cookies.isKey("cookieHp")) {
        this.slider_hp = this.$cookies.get("cookieHp");
      }
    },
    watch: {
      'slider_lv': 'setCookieLv',
      'slider_hp': 'setCookieHp'
    }
  }
</script>
<style scoped>
#copyBtn {
  position: absolute;
  right: 0;
}
</style>