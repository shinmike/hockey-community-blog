<template>
  <div>
    <div style="background: #048334">
      <img src="../assets/hc.png" />
    </div>
    <nav class="sans-serif f5 lh-copy mid-gray center">
      <ul>
        <li><router-link to="/" exact>Blog</router-link></li>
        <li><router-link to="/add" exact>Add a new blog</router-link></li>
      </ul>
    </nav>
  </div>
</template>

<script>

  export default{}

</script>

<style scoped>
  ul{
    list-style-type: none;
    text-align: center;
    margin: 0;
  }
  li{
      display: inline-block;
      margin: 0 10px;
  }
  a{
      color: #fff;
      text-decoration: none;
      padding: 6px 8px;
      border-radius: 10px;
  }
  nav{
      background:#009546;
      padding: 14px 0;
      margin-bottom: 40px;
  }
  .router-link-active{
      background: #eee;
      color: #444;
  }
  img {
    height: 50px; 
    width: 50px; 
    display: block; /*for the img inside your div */  
    margin-left: auto ;
    margin-right: auto;
  }
</style>