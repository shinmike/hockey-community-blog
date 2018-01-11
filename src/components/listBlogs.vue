<template>
  <div id="show-blogs">
    <h1>List Blog Titles</h1>
    <input type="text" placeholder="search blogs" v-model="search" />
    <div v-for="blog in filteredBlogs" class="single-blog">
      <h2 v-rainbow>{{blog.title | to-uppercase}}</h2>
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
    this.$http.get('https://jsonplaceholder.typicode.com/posts').then(function(data){
      this.blogs = data.body.slice(0,10);
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
