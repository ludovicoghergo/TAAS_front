<template>
  <div>
    <v-row v-for="(answer, index) in answers" :key="index">
      <v-col cols="12" class="d-flex justify-center">
        <v-card color="#f4ecb4" class="mt-2 answer">
          <v-card-title class="headline"> Nome tizio</v-card-title>

          <v-card-text>{{ answer.text }}</v-card-text>

          <v-card-actions class="card-actions">
            <v-btn text> da fare</v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Answers",
  components: {},
  props: ["id"],
  data() {
    return {
      answers: [],
    };
  },

  mounted() {
    var vm = this;
    axios
      .get("http://localhost:8081/api/querys/" + vm.id + "/answers")
      .then(function (response) {
        vm.answers = response.data;
      })
      .catch((error) => {
        if (error.response) {
          // The request was made and the server responded with a status code
          // that falls out of the range of 2xx
          console.log(error.response.data);
          console.log(error.response.status);
          console.log(error.response.headers);
        } else if (error.request) {
          // The request was made but no response was received
          // `error.request` is an instance of XMLHttpRequest in the browser and an instance of
          // http.ClientRequest in node.js
          console.log(error.request);
        } else {
          // Something happened in setting up the request that triggered an Error
          console.log("Error", error.message);
        }
      });
  },
};
</script>
<style scoped>
.answer {
  height: 30vh;
  width: 70vw;
  margin-left: auto;
  margin-right: auto;
}
.card-actions {
  position: absolute;
  bottom: 0;
}
</style>

