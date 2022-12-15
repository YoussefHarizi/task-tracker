<template>
    <button :style="{background:color}" class="btn" @click="$emit('clicked-btn')">{{text}}</button>
</template>
<script>
export default {
    name:"Button",
  
    props:{
        text:String,
        color:String
    }
   
}
</script>