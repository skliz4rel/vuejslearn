<template>
    <div>
    <h1>{{ headvalue }}  </h1>

        <p>{{ headtip }}</p>
    </div>
</template>





<script>

   export default 
   {
       props:[
           'headvalue',
           'headtip'
       ]
   }

</script>