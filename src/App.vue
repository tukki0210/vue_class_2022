<template>
  <BookList v-bind:title="title" v-bind:url="ImageUrl" />
  <BookCard v-bind:bookData = "bookData" />
  <!-- コンポーネントへのv-forの場合、複製されたコンポーネントを区別する重複しないkey属性が必要 -->
  <BookCard v-for="book in books"
            v-bind:bookData = "book.Item" 
            v-bind:key="book.Item.isbn" />

  <!-- P.88 v-forから配列要素だけでなく、その配列の各キーやインデックス番号が取れる -->
  <BookCard v-for="(book, key,index ) in books"
            v-bind:bookData = "book.Item" 
            v-bind:key="index" />
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
     bookData : {}, //空のオブジェクト
     books : [], // 空の配列
    }
  },
  // ライフサイクルフック（実行タイミングの指定）
  // 非同期処理を含む関数はmountedの中にに書く
  mounted: function () {
    const RAKUTEN_API = 'https://app.rakuten.co.jp/services/api/BooksBook/Search/20170404?format=json&title=programing&booksGenreId=001&applicationId=1024837784734370415'
    fetch(RAKUTEN_API)
      .then(response => response.json())
      .then(data => {
        // 複数の本のデータが入った配列
        const books = data.Items
        this.books = books

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
