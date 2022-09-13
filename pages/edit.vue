<template>
  <div class="container">
    <div class="card">
      <h2 class="card-header">Edit Article</h2>
      <div class="card-body">
        <div class="row">
          <div class="col-md-12">
            <label>Article Title</label>
            <input
              type="text"
              name="title"
              v-model="title"
              class="form-control"
            />
          </div>
          <div class="col-md-12">
            <label>Article Content</label>
            <textarea
              name="content"
              class="form-control"
              v-model="content"
              id=""
              cols="30"
              rows="10"
            ></textarea>
          </div>
          <div class="col-md-12">
            <button class="btn btn-success" @click="updateArticle">
              Update
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: "",
      content: "",
      key: "",
      article: null,
    };
  },
  mounted() {
    this.getArticle();
  },
  methods: {
    getArticle() {
      let vm = this;
      let article_list = localStorage.getItem("article_list");
      article_list = JSON.parse(article_list);
      this.id = this.$route.params.id;
      article_list = article_list.filter((item, key) => {
        return key == vm.id;
      });
      console.log(article_list);
      this.title = article_list[0].title;
      this.content = article_list[0].content;
    },
    updateArticle() {
      let article_list = localStorage.getItem("article_list");
      article_list = JSON.parse(article_list);

      console.log(article_list[this.id]);

      article_list[this.id].title = this.title;
      article_list[this.id].content = this.content;
      article_list[this.id].date = new Date();

      localStorage.setItem("article_list", JSON.stringify(article_list));
      location.href = "/";
    },
  },
};
</script>

<style>
</style>
