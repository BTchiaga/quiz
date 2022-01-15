<template>
<v-app>
    <v-main>
      <Header
      :numCorrect="numCorrect"
      :numTotal="numTotal"/>
      <v-container class="">
      <v-row no-gutters>
        <v-col sm="3" ></v-col>
        <QuestionCard v-if="Questions.length" :currentQuestion="Questions[index]" 
        :next="next"
        :increment="increment"/>

      </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import Header from './components/Header';
import QuestionCard from './components/QuestionCard';

export default {
  name: 'App',

  components: {
    Header,
    QuestionCard
  },

  data () {
    return {
Questions:[],
index:0,
numCorrect:0,
numTotal:0
    }
  },
  methods: {
    next(){
      this.index+=1
    },
    increment(isCorrect){
      if(isCorrect){
        this.numCorrect += 1
        
    }
    this.numTotal += 1

  

    }
  },
  mounted() {
    fetch('https://opentdb.com/api.php?amount=7&category=18&difficulty=medium&type=multiple', {method:"get"}).then((response) => {
     return response.json()
    }
    ).then((jsonData)=>{
this.Questions= jsonData.results
    })},
};
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #295f94;
  margin-top: 60px;
}

</style>
