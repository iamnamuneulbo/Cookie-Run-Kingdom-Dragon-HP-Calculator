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
      thumb-label
      min="1"
      :max="maxLv"
    >
    <template v-slot:append>
                <v-text-field
                  v-model="slider_lv"
                  class="mt-0 pt-0"
                  type="number"
                  style="width: 60px"
                  :max="maxLv"
                  @input="updateValue"
                ></v-text-field>
              </template>
    </v-slider>
    
    <h3>
      Dragon HP(%)
    </h3>
    <v-slider
      v-model="slider_hp"
      thumb-label
      min="1"
      max="99"
    >
    <template v-slot:append>
                <v-text-field
                  v-model="slider_hp"
                  class="mt-0 pt-0"
                  type="number"
                  style="width: 60px"
                ></v-text-field>
              </template>
    </v-slider>

    <h3>
      Full HP
    </h3>
    <p class="pl-2 pb-4">
      Lv.{{slider_lv}} | {{dragonHP[slider_lv].toLocaleString()}} | {{Math.floor(dragonHP[slider_lv] / 1000)}}K
    </p>

    <h3>
      Left HP
    </h3>
    <p class="pl-2">
      {{calMinHP().toLocaleString()}} ~ {{calMaxHP().toLocaleString()}}<br/>
      {{Math.floor(calMinHP() / 1000)}}K ~ {{Math.floor(calMaxHP() / 1000)}}K
    </p>
  </v-container>
</template>

<script>
  export default {
    name: 'CookieRun',

    data: () => ({
      maxLv: 60,
      slider_lv: 20,
      slider_hp: 50,
      dragonHP: [
        0,
        3000000,
        3150000,
        3474000,
        3648000,
        3830000,
        4022200,
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
        51098000,
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
      updateValue() {
        if (this.maxLv < this.slider_lv) {
          this.slider_lv = this.maxLv;
        }
        this.$forceUpdate()
      },
      calMinHP() {
        return this.dragonHP[this.slider_lv] * this.slider_hp / 100
      },
      calMaxHP() {
        return this.dragonHP[this.slider_lv] * (this.slider_hp + 1) / 100 - 1
      }
    }
  }
</script>
