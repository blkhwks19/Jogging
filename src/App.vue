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
                <v-row class="mx-1">
                  <v-spacer></v-spacer>
                  <v-select
                    v-model="warmTime"
                    :items="times"
                    hide-details
                    single-line
                    :disabled="!warmSwitch"
                  >
                    <template v-slot:prepend>
                      <v-icon :class="{'primary--text':warmSwitch}">mdi-timer-outline</v-icon>
                    </template>
                  </v-select>
                </v-row>
              </v-card-text>
            </v-card>
          </v-col>

          <v-col cols="12" v-for="(block, i) in blocks" :key="block.id">
            <v-card>
              <v-card-title>
                #{{i+1}}
                <v-spacer></v-spacer>
                <v-btn 
                  icon 
                  color="error"
                  @click="deleteBlock(block.id)">
                  <v-icon>mdi-delete</v-icon>
                </v-btn>
              </v-card-title>
              <v-card-text>
                <v-row class="mx-1" align="end">
                  <span class="headline">Jog</span>
                  <v-spacer></v-spacer>
                  <v-select
                    v-model="block.jogTime"
                    :items="times"
                    hide-details
                    single-line
                  >
                    <template v-slot:prepend>
                      <v-icon color="primary">mdi-timer-outline</v-icon>
                    </template>
                  </v-select>
                </v-row>
                <v-row class="mx-1" align="end">
                  <span class="headline">Walk</span>
                  <v-spacer></v-spacer>
                  <v-select
                    v-model="block.walkTime"
                    :items="times"
                    hide-details
                    single-line
                  >
                    <template v-slot:prepend>
                      <v-icon color="primary">mdi-timer-outline</v-icon>
                    </template>
                  </v-select>
                </v-row>
                <v-row class="mx-1" align="end">
                  <span class="headline">Repeat</span>
                  <v-spacer></v-spacer>
                  <v-select
                    v-model="block.repeat"
                    :items="repeatTimes"
                    hide-details
                    single-line
                    class="mr-1"
                  >
                    <template v-slot:prepend>
                      <v-icon :class="{'primary--text':coolSwitch}">mdi-repeat</v-icon>
                    </template>
                  </v-select>
                  <span v-if="block.repeat === 1" class="title">time</span>
                  <span v-else class="title">times</span>
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
                <v-row class="mx-1">
                  <v-spacer></v-spacer>
                  <v-select
                    v-model="coolTime"
                    :items="times"
                    hide-details
                    single-line
                    :disabled="!coolSwitch"
                  >
                    <template v-slot:prepend>
                      <v-icon :class="{'primary--text':coolSwitch}">mdi-timer-outline</v-icon>
                    </template>
                  </v-select>
                </v-row>
              </v-card-text>
            </v-card>
          </v-col>


        </v-row>

        <v-btn
          fab
          fixed
          bottom
          left
          color="success"
          @click="addBlock()"
        >
          <v-icon>mdi-plus</v-icon>
        </v-btn>

        <v-btn
          fab
          fixed
          bottom
          right
          color="primary"
          @click="go()"
        >
          <v-icon>mdi-run-fast</v-icon>
        </v-btn>

      </v-container>
    </v-content>
  </v-app>
</template>

<script>
import {v4 as uuidv4} from 'uuid';

export default {
  name: 'App',

  data: () => ({
    times: [],
    blocks: [],
    repeatTimes: [1,2,3,4,5,6,7,8,9,10],

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

    addBlock() {
      const block = {
        id: uuidv4(),
        jogTime: '1:00',
        walkTime: '1:00',
        repeat: 1,
      }
      this.blocks.push(block);
    },

    deleteBlock(id) {
      this.blocks = this.blocks.filter(block => block.id !== id);
    },

    go() {
      


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
