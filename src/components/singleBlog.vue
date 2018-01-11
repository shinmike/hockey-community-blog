<template>
  <div id="single-blog" class="sans-serif f5 lh-copy mid-gray center">
    <h1>{{blog.title}}</h1>
    <article style="white-space: pre-line;">{{blog.content}}</article>
    <p>Author: {{blog.author}}</p>
    <p>Category: </p>
    <ul>
      <li v-for="category in blog.categories">{{category}}</li>
    </ul>
  </div>
</template>

<script>
  export default {
    data(){
      return {
        id: this.$route.params.id,
        blog: {}
      }
    },
    created(){
      this.$http.get('https://vuejs-simple.firebaseio.com/posts/'+ this.id + '.json').then(function(data){
        return data.json();
      }).then(function(data){
        this.blog = data;
      });
    }
  }
</script>
<style scoped>
  #single-blog {
    max-width: 960px;
    margin: 0 auto;
    padding: 0 20px;
  }
  
</style>