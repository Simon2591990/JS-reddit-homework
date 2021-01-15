<template lang="html">
  <div id="app">
    <h1>{{posts[0].data.subreddit_name_prefixed}}</h1>
    <!-- <h2>{{posts[10].data.title}}</h2>
    <p>{{posts[10].data.selftext}}</p>
    <img :src="posts[10].data.url" alt="Cant Load Image"> -->
    <form v-on:submit.prevent="getPosts">
    <input type="text" v-model="subreddit">
    <button type="submit">Button</button>
    </form>   
    <post-list :postList="posts"></post-list>
        
  </div>
</template>

<script>
import PostList from './components/PostList.vue'

export default {
  name: 'App',
  components: {
    "post-list": PostList
    
  },
  data(){
    return {
      subreddit: 'ProgrammerHumor',
      posts: null
    }
  },
  methods:{
      getPosts: function(){
        fetch(`https://www.reddit.com/r/${this.subreddit}.json`)
        .then(res => res.json())
        .then(data => this.posts = data.data.children)
      },
        
    },
  mounted(){
    this.getPosts()      
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
  margin-top: 60px;
  background-color: black;
  
}
img{
  width: 700px
}
</style>
