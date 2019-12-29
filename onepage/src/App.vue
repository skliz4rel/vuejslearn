<template>
  <div id="app">

    <Header    
    :headvalue="headvalue"
     :headtip = "headtip"/>

    <Content :body="body"
      :welcome="welcome"
      :questions="questions"
      :currentQuestion = "currentQuestion"
     />
   
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Content from './components/Content.vue'

export default {
  name: 'app',
  components: {
    Header,
    Content
  },
  data(){
    return {
       headvalue:'Service  POS',
       headtip:'',
       body:'This is the body',
       welcome:'',
       questions:[],
       index:0,
       currentQuestion: Object
    }
  },
 watch:{
      
        currentQuestion:{
            immediate:true,
            handler(){
                this.index= 0;
                this.currentQuestion = this.questions[this.index]
            }
        }
    },

  methods:{
    displayWelcome(){
      this.headtip = 'For Service oriented businesses'
      this.welcome = 'Welcome to my app'
    },
    getQuestions: function(){
     
       fetch('http://localhost:8080/json/index.php', {
        method: 'get'
    })
    .then((response) => {
       return response.json()
    })
    .then((jsonData) => {
        alert(jsonData);
      if(jsonData.result === 'success'){
        this.questions  = jsonData.questions;
      }
    })
    }
  },
  mounted:function(){
     this.displayWelcome()
     this.getQuestions()
  },
created: function(){
			//console.log(this.questions.length);
		}
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>