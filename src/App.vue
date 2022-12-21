<template>
  <!-- <BookCard v-for="book in books"
            v-bind:bookData = "book.Item" 
            v-bind:key="book.Item.isbn" /> -->

  <HotelCard v-for="(hotel,key,index) in hotels" 
              v-bind:hotelData = "hotel.hotel"
              v-bind:key="index" />
</template>

<script>
// import BookCard from './components/BookCard.vue'
import HotelCard from './components/HotelCard.vue'

export default {
  name: 'App',
  components: {
    // BookCard,
    HotelCard
  },
  data () {
    return {
     books : [], // 空の配列
     hotels :[]
    }
  },
  mounted: function () {
    const RAKUTEN_API = 'https://app.rakuten.co.jp/services/api/BooksBook/Search/20170404?format=json&title=javascript&booksGenreId=001&applicationId=1024837784734370415'
    fetch(RAKUTEN_API)
      .then(response => response.json())
      .then(data => {
        console.log(data)
        // 複数の本のデータが入った配列
        const books = data.Items
        this.books = books

      })

    const RAKUTEN_HOTEL_API = "https://app.rakuten.co.jp/services/api/Travel/SimpleHotelSearch/20170426?format=json&largeClassCode=japan&middleClassCode=nara&smallClassCode=nara&applicationId=1024837784734370415"
    fetch(RAKUTEN_HOTEL_API)
      .then(res => res.json())
      .then(data => {
        // 取れているか確認
        console.log(data)
        // 複数のホテルのデータが入った配列
        const hotels = data.hotels
        // data()のhotelsにコピー
        this.hotels = hotels
      })
    }
}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
