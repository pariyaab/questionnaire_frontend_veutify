<template>
  <v-app>
    <v-row>
      <v-col cols="12" md="10" class="pa-16">
        <div class="d-flex pt-8 justify-center align-center" style="height: 100%">
          <div class="mt-n16" style="width: 100%">
            <h1  style="color: #ffb300">
              welcome to our rating system
            </h1>
            <v-row class="mt-16">
              <v-col cols="12" md="8">
                <v-row>
                  <v-col cols="12" md="3">
                    <h2 class="mx-5 mt-3">First Name:</h2>
                  </v-col>
                  <v-col cols="12" md="9">
                    <v-text-field
                        outlined
                    ></v-text-field>
                  </v-col>
                </v-row>
                <v-row>
                  <v-col cols="12" md="3">
                    <h2 class="mx-5 mt-3">Last Name:</h2>
                  </v-col>
                  <v-col cols="12" md="9">
                    <v-text-field
                        outlined
                    ></v-text-field>
                  </v-col>
                </v-row>
                <v-row>
                  <v-col cols="12" md="3">
                  </v-col>
                  <v-col cols="12" md="9">
                    <v-btn class="white--text elevation-0 " x-large block tile color="#ffb300"> let's go</v-btn>
                  </v-col>
                </v-row>
              </v-col>

            </v-row>
          </div>
        </div>
      </v-col>
      <v-col cols="12" md="2" class="base d-flex flex-column justify-end">
        <div class="d-flex justify-center align-end">
          <v-img src="@/assets/Questions-rafiki.svg"></v-img>
        </div>
      </v-col>
    </v-row>
  </v-app>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

@Component({
  components: {},
})
export default class AboutView extends Vue {
  value = "50%";
}
</script>
<style>
.base {
  background-color: #f3f3f3;
}
</style>
