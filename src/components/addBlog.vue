<template>
  <div id="add-blog" class="sans-serif f5 lh-copy mid-gray center">
    <h2>Add a New Blog Post</h2>
    <form v-if="!submitted">
      <label>Blog Title:</label>
      <input type="text" v-model.lazy="blog.title" required />
      <label>Blog Content</label>
      <textarea v-model.lazy="blog.content"></textarea>
      <div id="checkboxes">
        <label>Gear</label>
        <input type="checkbox" value="gear" v-model="blog.categories"/>
        <label>News</label>
        <input type="checkbox" value="news" v-model="blog.categories"/>
        <label>Reviews</label>
        <input type="checkbox" value="reviews" v-model="blog.categories"/>
        <label>Events</label>
        <input type="checkbox" value="events" v-model="blog.categories"/>
      </div>
      <label>Author:</label>
      <select v-model="blog.author">
        <option v-for="author in authors">{{author}}</option>
      </select>
      <button v-on:click.prevent="post">Add Blog</button>
    </form>
    <div v-if="submitted">
      <h3>Thanks for adding your post</h3>
    </div>
    <div id="preview">
      <h3>Preview Blog</h3>
      <p>Blog title: {{blog.title}} </p>
      <p>Blog content:</p>
      <p style="white-space: pre-line; font-style: italic">{{blog.content}}</p>
      <p>Blog Categories: </p>
      <ul>
        <li v-for="category in blog.categories">{{category}}</li>
      </ul>
      <p>Author: {{blog.author}}</p>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      blog: {
        title: "",
        content: "",
        categories: [],
        author: ""
      },
      authors: ['Michael', 'Jack', 'Amrit', 'Ryan'],
      submitted: false,
    }
  },
  methods: {
    post: function(){
      this.$http.post('https://vuejs-simple.firebaseio.com/posts.json', this.blog).then(function(data){
        console.log(data);
        this.submitted = true;
      })
    }
  }
}
</script>

<style>
  #add-blog *{
      box-sizing: border-box;
  }
  #add-blog{
      margin: 20px auto;
      max-width: 500px;
  }
  label{
      display: block;
      margin: 20px 0 10px;
  }
  input[type="text"], textarea{
      display: block;
      width: 100%;
      padding: 8px;
  }
  #preview{
      padding: 10px 20px;
      border: 1px dotted #ccc;
      margin: 30px 0;
  }
  h3{
      margin-top: 10px;
  }

  #checkboxes input {
    display: inline-block;
    margin-right: 10px;
  }

  #checkboxes label {
    display: inline-block;
  }
</style>