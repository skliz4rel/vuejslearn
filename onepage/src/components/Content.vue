<template>
    <div>
        <h2>
            {{ welcome }}
        </h2>

        <div>
            <h3>Total Questions {{ questions.length }}</h3>

           
        </div>
    </div>
</template>

<script>

 export default {

       props:{
           'welcome':[],       
            questions:Array, 
            currentQuestion:Object
       },
       data(){
           return {
                questionNo:0
           }
       },
       methods:{
           countQuestion: function(){
               this.questionNo = this.questions.length;
           }

       },
       mounted:{


       }
   }


</script>