<template>
  <v-app>
    <v-row>

      <v-col cols="12" md="10" class="pa-16 d-flex flex-column justify-space-between">
        <div>
          <div class="d-flex  justify-end">
            <h2 class="font-weight-bold" style="color: #ff8f00">Question {{ questions_id + 1 }}/50</h2>
          </div>

          <v-row>
            <v-col cols="12" md="8">
              <v-row>
                <v-col cols="12" md="3">
                  <h2 class="mx-5 mt-3">List Name:</h2>
                </v-col>
                <v-col cols="12" md="9">
                  <p>
                    {{ lists[questions_id][0].list_name}}
                  </p>
                </v-col>
              </v-row>
              <v-row>
                <v-col cols="12" md="3">
                  <h2 class="mx-5 mt-3">Link:</h2>
                </v-col>
                <v-col cols="12" md="9">
                  <p>
                    <a :href="link + lists[questions_id][0].list_id"> {{ link + lists[questions_id][0].list_id }}</a>
                  </p>
                </v-col>
              </v-row>
              <v-row>
                <v-col cols="12" md="3">
                  <h2 class="mx-5 mt-3">explanation:</h2>
                </v-col>
                <v-col cols="12" md="9">
                  <v-textarea
                      outlined :value="explanations_list[questions_id][0].text"
                  ></v-textarea>
                </v-col>
              </v-row>
            </v-col>
          </v-row>

          <div class="mx-4 mx-md-16 mt-16">
            <h1 style="color: #ffb300">
              Please Choose One Answer !
            </h1>

            <v-radio-group v-model="radioGroup">
              <v-radio label="Explanation is relevant and contains information " :value="1"
                       v-model="answer_id"></v-radio>
              <v-radio label="Explanation is relevant but contains no information " :value="2"></v-radio>
              <v-radio label="Explanation is not relevant " :value="3"></v-radio>
              <v-radio label="I have no answer " :value="4"></v-radio>
            </v-radio-group>
          </div>
        </div>
        <div class="d-flex flex-wrap justify-space-between">
          <div class="mt-3 mt-md-0" style="opacity: 5% ;">
            <v-avatar color="indigo">
              <v-icon dark>
                mdi-arrow-left
              </v-icon>
            </v-avatar>
            <span class="mx-4 font-weight-bold ">Previous Question</span>
          </div>
          <div class="mt-3 mt-md-0" @click="load_next_question">
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
              v-model="value"
              :total-steps="30"
              class="font-weight-bold"
          >

            <div class="d-flex align-center flex-column justify-center">
              <h2>{{ value }} %</h2>

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
import axios from "axios"

@Component({
  components: {},
})
export default class HomeView extends Vue {

  explanations_list = [];
  temp = 20
  lists = [];
  questions_id = 0;
  answer_id = 1
  results = [];
  questions_bind = {};
  link = "https://twitter.com/i/lists/"
  radioGroup = 1
  token = ""

  created() {

    this.token = "Bearer " + this.$cookies.get('user').token
    console.log(this.token);

    this.getQuestions()
  }

  get value(): number {
   return Math.floor(( (Number(this.questions_id) + 1) * 100 / 50 ))
  }

  async getQuestions() {
    await axios.get(
        "http://127.0.0.1:8000/list",
        {
          headers: {
            authorization:
            this.token
          },
        }
    )
        .then((response) => {
          this.explanations_list = response.data.explanations;
          this.lists = response.data.lists;

          console.log("explanations: ", this.explanations_list[0][0]);
          console.log("lists: ", this.lists);
        })
        .catch((error) => {
          console.log(error);
        });
  }

  load_next_question() {
    
    console.log(this.radioGroup);
    this.sendAnswer()
    this.questions_id++;
  }

  async sendAnswer() {

    const formData = {
      explanation: this.explanations_list[this.questions_id][0]["id"],
      answer_id: this.radioGroup,
      list_id : this.lists[this.questions_id][0]["id"]
    }
    console.log(formData);
    const response = await axios.post("http://127.0.0.1:8000/add", formData, {
      headers: {
        authorization: this.token,
        'Content-Type': 'multipart/form-data'
      }
    });
    if (response.status == 200) {
      console.log("successfully added");
    }
  }
}


</script>
<style scoped>
.base {
  background-color: #f3f3f3;
}
p {
  font-size: 1.2rem;
  margin-top: 0.6em;
  margin-bottom: 0em;
  border: 1px solid rgba(112, 112, 112, 0.5);
  padding: 20px;
  border-radius: 5px;
}
</style>
