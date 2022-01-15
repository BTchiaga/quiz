<template>
    <div>
        <v-app-bar app tabs color="#6A76AB"
 dense
>
<v-app-bar-title>
    Test Quiz App

</v-app-bar-title>

        <div class="mx-2"><b> </b></div>
        <div>Counter : {{numCorrect}} / {{numTotal}}</div>
        </v-app-bar>
    </div>
</template>
<script>
export default {
    props:[
'numCorrect',
 'numTotal'    
 ]  
}    
</script>
<style scoped>
.v-toolbar__content{
    text-align: center;
}
</style>