<template>
  <div class="container">
    <div class="card">
      <h2 class="card-header">Add Article</h2>
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
            <button class="btn btn-success" @click="postArticle">POST</button>
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
    };
  },
  methods: {
    postArticle() {
      //   localStorage.removeItem("article_list");
      let article_list = localStorage.getItem("article_list");
      article_list = JSON.parse(article_list);
      console.log("art", article_list);

      let payload = {
        title: this.title,
        content: this.content,
        date: new Date(),
      };

      if (article_list !== null && article_list !== "null") {
        article_list = [
          ...article_list,
          {
            title: this.title,
            content: this.content,
            date: new Date(),
          },
        ];
      } else {
        article_list = [
          {
            title: this.title,
            content: this.content,
            date: new Date(),
          },
        ];
      }

      localStorage.setItem("article_list", JSON.stringify(article_list));

      location.href="/";
    },
  },
};
</script>

<style>
</style>
