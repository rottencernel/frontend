<template>
  <div class="container">
    <div class="row">
      <div class="col-lg-8">
        <h1 class="breadcrumb-item active" aria-current="page">{{ post.title }}</h1>
        <img class="img-fluid rounded " :src="post.image" alt=""/>
        <hr>
        <p v-html="post.content"></p>
        <hr>
        <div class="d-flex">
          <div class="mr-auto p-2 lead">Автор: {{ post.author }}</div>
          <div class="p-2">Опубликовано: {{ post.published }}</div>
        </div>
        <hr>
          <Comments :comments="comments" :post="post"/>
      </div>
    </div>
  </div>
 
</template>

<script>
import axios from "axios";
import Comments from "@/components/Comments";
export default {
  components: {
    Comments
  },

  async asyncData({ params }) {
    try {
      const post = await axios.get(`http://127.0.0.1:8000/api/posts/${params.slug}`);
      const comments = await axios.get(`http://127.0.0.1:8000/api/comments/${params.slug}`);

      post.data.published = `${new Date( Date.parse(post.data.published) )}`.split('G')[0]
  
      return {
        post: post.data,
        comments: comments.data
      }
    }

    catch(err) {
      return {
        error: err,
        errorMessage: 'Что-то пошло не так...'
      }
    }
  },
}
</script>

<style scoped>

</style>