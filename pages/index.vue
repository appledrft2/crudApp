<template>
  <div class="container">
    <h1>Simple Bulletin Board</h1>
    <nuxt-link to="/add" class="btn btn-primary">Create New Article</nuxt-link>
    <table class="table table-bordered">
      <thead>
        <tr>
          <th>Article Title</th>
          <th>Article Content Snippet</th>
          <th>Created Date</th>
          <th></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(article, key) in article_list">
          <td>{{ article.title }}</td>
          <td>{{ article.content }}</td>
          <td>{{ article.date }}</td>
          <td>
            <NuxtLink class="btn btn-success" :to="`/edit/${key}`"
              >Edit</NuxtLink
            >
            <button class="btn btn-danger" @click="deleteArticle(key )">
              Delete
            </button>
          </td>
        </tr>
        <tr v-if="article_list.length === 0">
          <td colspan="4">No Records Found</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<script>
export default {
  data() {
    return {
      article_list: [],
    };
  },
  mounted() {
    this.getArticleList();
  },
  methods: {
    getArticleList() {
      let list = localStorage.getItem("article_list") || [];
      this.article_list = JSON.parse(list);
    },
    deleteArticle(key) {
 
     this.article_list.splice(key, 1);
  
        localStorage.setItem("article_list", JSON.stringify(this.article_list));
    },
  },
};
</script>
<style scoped>
</style>