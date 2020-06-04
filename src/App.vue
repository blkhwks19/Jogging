<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png"
          transition="scale-transition"
          width="40"
        />

        <v-img
          alt="Vuetify Name"
          class="shrink mt-1 hidden-sm-and-down"
          contain
          min-width="100"
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-name-dark.png"
          width="100"
        />
      </div>

      <v-spacer></v-spacer>

      <v-btn
        href="https://github.com/vuetifyjs/vuetify/releases/latest"
        target="_blank"
        text
      >
        <span class="mr-2">Latest Release</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar>

    <v-content>
      <v-container>
        <v-row justify-content="center">
        
          <v-col cols="12">
            <v-card>
              <v-card-title>
                Warmup
                <v-spacer></v-spacer>
                <v-switch
                  v-model="warmSwitch"
                  color="success"
                  hide-details
                ></v-switch>
              </v-card-title>
              <v-card-text>
                <v-row>
                  <v-spacer></v-spacer>
                  <v-select
                    v-model="warmTime"
                    :items="times"
                    hide-details
                    prepend-icon="mdi-timer-outline"
                    single-line
                  ></v-select>
                </v-row>
              </v-card-text>
            </v-card>
          </v-col>

          

          <v-col cols="12">
            <v-card>
              <v-card-title>
                Cooldown
                <v-spacer></v-spacer>
                <v-switch
                  v-model="coolSwitch"
                  color="success"
                  hide-details
                ></v-switch>
              </v-card-title>
              <v-card-text>
                <v-row>
                  <v-spacer></v-spacer>
                  <v-select
                    v-model="coolTime"
                    :items="times"
                    hide-details
                    prepend-icon="mdi-timer-outline"
                    single-line
                  ></v-select>
                </v-row>
              </v-card-text>
            </v-card>
          </v-col>

        </v-row>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
export default {
  name: 'App',

  data: () => ({
    times: [],

    warmSwitch: false,
    warmTime: '5:00',

    coolSwitch: false,
    coolTime: '5:00',
  }),

  created() {
    this.createTimes();
  },

  methods: {
    createTimes() {
      for (let i = 0; i <= 1200; i += 5) {
        this.times.push(this.secToMinSec(i));
      }
    },

    secToMinSec(s) {
      let min = Math.floor(parseInt(s) / 60);
      let sec = s - (min * 60);
      sec = (sec < 10) ? `0${sec}` : sec;
      return `${min}:${sec}`;
    },
  }
};
</script>

<style scoped>
.theme--light.v-application {
  background-color: #ddd;
}

.v-input--selection-controls {
  margin-top: 0;
}
</style>
