<template>
  <v-app>
    <v-row>

      <v-col cols="12" md="10" class="pa-16 d-flex flex-column justify-space-between">
       <div>
         <div class="d-flex  justify-end">
           <h2 class="font-weight-bold" style="color: #ff8f00">Question 15/30</h2>
         </div>

         <v-row>
           <v-col cols="12" md="8">
             <v-row>
               <v-col cols="12" md="3">
                 <h2 class="mx-5 mt-3">List Name:</h2>
               </v-col>
               <v-col cols="12" md="9">
                 <v-text-field
                     outlined
                 ></v-text-field>
               </v-col>
             </v-row>
             <v-row>
               <v-col cols="12" md="3">
                 <h2 class="mx-5 mt-3">Link:</h2>
               </v-col>
               <v-col cols="12" md="9">
                 <v-text-field
                     outlined
                 ></v-text-field>
               </v-col>
             </v-row>
             <v-row>
               <v-col cols="12" md="3">
                 <h2 class="mx-5 mt-3">explanations:</h2>
               </v-col>
               <v-col cols="12" md="9">
                 <v-text-field
                     outlined
                 ></v-text-field>
               </v-col>
             </v-row>
           </v-col>
         </v-row>

         <div class="mx-4 mx-md-16 mt-16">
           <h1 style="color: #ffb300">
             is list related to explanation and th links given?
           </h1>

           <v-radio-group v-model="radioGroup">
             <v-radio label="this is for label question " :value="1"></v-radio>
             <v-radio label="this is for label question " :value="2"></v-radio>
             <v-radio label="this is for label question " :value="3"></v-radio>
           </v-radio-group>
         </div>
       </div>
        <div class="d-flex flex-wrap justify-space-between">
          <div class="mt-3 mt-md-0">
            <v-avatar color="indigo">
              <v-icon dark>
                mdi-arrow-left
              </v-icon>
            </v-avatar>
            <span class="mx-4 font-weight-bold ">Previous Question</span>
          </div>
          <div class="mt-3 mt-md-0">
            <v-avatar color="indigo">
              <v-icon dark>
                mdi-arrow-right
              </v-icon>
            </v-avatar>
            <span class="mx-4 font-weight-bold ">Next Question</span>
          </div>
        </div>
      </v-col>

      <v-col cols="12" md="2" class="base d-flex flex-column justify-space-between">
        <div class="d-flex align-start justify-center pt-5">
          <v-progress-circular
              :rotate="90"
              :width="16"
              :size="180"
              color="orange lighten-2"
              :value="value"
              class="font-weight-bold"
          >
            <div class="d-flex align-center flex-column justify-center">
              <h2>{{ value }}</h2>

              <span> <h2>completed</h2> </span>
            </div>
          </v-progress-circular>
        </div
        >
        <div class="d-flex justify-center align-end">
          <v-img src="@/assets/Questions-rafiki.svg"></v-img
          >
        </div>
      </v-col>
    </v-row>
  </v-app>
</template>

<script lang="ts">
import {Component, Vue} from "vue-property-decorator";

@Component({
  components: {},
})
export default class HomeView extends Vue {
  value = "50%";
  radioGroup = 1
}
</script>
<style>
.base {
  background-color: #f3f3f3;
}
</style>
