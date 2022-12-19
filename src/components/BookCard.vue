<template>
    <div>
        <img v-bind:src="bookData.mediumImageUrl" alt="">
        <div>{{bookData.title}}</div>
    </div>
</template>
<script>
export default {
    name:'BookCard',
    props:{
        bookData:Object
    }
}
</script>
<style>
    
</style>