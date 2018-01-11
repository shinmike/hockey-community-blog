<template>
  <div id="show-blogs" class="sans-serif f5 lh-copy mid-gray center">
    <h1 class="f1 lh-title">All Blog Articles</h1>
    <input type="text" placeholder="search blogs" v-model="search" />
    <div v-for="blog in filteredBlogs" class="single-blog">
      <router-link v-bind:to="'/blog/' + blog.id"><h2 class="f2 lh-copy">{{blog.title | to-uppercase}}</h2></router-link>
      <article class="f4 lh-copy">{{blog.content | snippet}}</article>
    </div>
  </div>
</template>

<script>
import searchMixin from '../mixins/searchMixins';

export default {

  data () {
    return {
      blogs: [],
      search: ""
    }
  },
  methods: {
    
  },
  created(){
    this.$http.get('https://vuejs-simple.firebaseio.com/posts.json').then(function(data){
      return data.json();
    }).then(function(data){
      var blogsArray = [];
      for (let key in data){
        data[key].id = key;
        blogsArray.push(data[key]);
      }
      this.blogs = blogsArray;
    })
  },
  computed: {

  },
  filters: {
    'to-uppercase': function(value){
      return value.toUpperCase();
    },
    'snippet': function(value){
      return value.slice(0, 100) + "...";
    },
  },
  mixins: [searchMixin]

}
</script>

<style>
  #show-blogs {
    max-width: 800px;
    margin: 0 auto;
  }

  .single-blog {
    padding: 20px;
    margin: 20px 0;
    box-sizing: border-box;
    background: #eee;
  }

</style>
