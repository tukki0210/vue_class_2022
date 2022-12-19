<template>
  <BookList v-bind:title="title" v-bind:url="ImageUrl" />
  <BookCard v-bind:bookData = "bookData" />
</template>

<script>
// import 外部ファイルを読み込む
import BookList from './components/BookList.vue'
import BookCard from './components/BookCard.vue'

// export 外部ファイルに公開する
export default {
  name: 'App',
  components: {
    BookList,
    BookCard
  },
  data () {
    return {
    // 初回ロード時に渡すダミーデータ
     title:'あああ',
     ImageUrl:'',
     bookData : {} //空のオブジェクト
    }
  },
  // ライフサイクルフック（実行タイミングの指定）
  // 非同期処理を含む関数はmountedの中にに書く
  mounted: function () {
    const RAKUTEN_API = 'https://app.rakuten.co.jp/services/api/BooksBook/Search/20170404?format=json&title=JavaScript&booksGenreId=001&applicationId=1024837784734370415'
    fetch(RAKUTEN_API)
      .then(response => response.json())
      .then(data => {
        // bookオブジェクトに指定した本の全データが入ってる
        const book = data.Items[1].Item
        // 非同期処理で取得したデータは、そのまま他のコンポーネントに渡せない
        // 本の名前を取得し、data()のtitleにコピー
        this.title = book.title
        this.ImageUrl = book.mediumImageUrl

        // 値の代わりにオブジェクトを渡す
        this.bookData = book
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
