<template>

  <div id="app">
    <ArticlePage></ArticlePage>
  </div>
</template>

<script>
import ArticlePage from './page/ArticleListPage.vue'
export default {
  name: 'App',
  components: {
    ArticlePage,
  }
}
</script>



<style>
#app {
  margin: 0;
}
</style>
