<template>
    <header>
        <h1>{{title}}</h1>
        <Button 
        :color="closeadd?'red':'blue'" 
        :text="closeadd?'Close':'Add Task'" 
        @clicked-btn="$emit('clicked-btn')"/>
    

        
    </header>
</template>
<script>
import Button from './Button.vue'


export default {
    name:'Header',
    components:{Button},
    props:{
        title:String,
        closeadd:Boolean,
    }
}
</script>
<style scoped>
header{
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
}
</style>