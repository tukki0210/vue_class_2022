<template>
    <div class="container">
        <img v-bind:src="BasicInfo.hotelImageUrl" alt="" hight="250" width="400"> 
        <div>
            <div>{{ BasicInfo.hotelName }}</div>
            <div>{{ BasicInfo.hotelSpecial }}</div>
            <div>{{ BasicInfo.access }}</div>
        </div>
    </div>
</template>
<script>
export default {
    name: 'HotelCard',
    props: {
        hotelData: Object
    },
    data(){
        return {
            BasicInfo:this.hotelData[0].hotelBasicInfo,
            RatingInfo:this.hotelData[1].hotelRatingInfo
        }
    }
}
</script>
<style>
.container {
    display: flex;
    flex-direction: row;
    border: solid 1px gray;
    margin: 0;
    padding: 5px;
    width: 1000px;
}
</style>