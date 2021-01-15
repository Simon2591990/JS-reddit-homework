<template lang="html">
  <div id="app">
    <h1>{{posts[0].data.subreddit_name_prefixed}}</h1>
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
      posts: []
    }
  },
    mounted(){
      this.getPosts()      
    },
  methods:{
      getPosts: function(){
        fetch(`https://www.reddit.com/r/${this.subreddit}/top.json`)
        .then(res => res.json())
        .then(allData => this.posts = allData.data.children)
      },
        
    },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: white;
  margin-top: 60px;
  background-color: black;
  
}

</style>
