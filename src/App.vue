<template lang="html">
  <div id="app">
    <h1>{{posts[0].data.subreddit_name_prefixed}}</h1>
    <form v-on:submit.prevent="getPosts">
    <input type="text" v-model="subreddit">
    <button type="submit">Search</button>
    </form>
    <button v-on:click="addToFavourites">Add Subreddit To Favourites</button>
    <favourite-subreddits :favouritesList="favouriteSubreddits"></favourite-subreddits>
    <post-list :postList="posts"></post-list>
        
  </div>
</template>

<script>
import PostList from './components/PostList.vue'
import FavouriteSubredditList from './components/FavouriteSubredditList.vue'


export default {
  name: 'App',
  components: {
    "post-list": PostList,
    "favourite-subreddits": FavouriteSubredditList
    
  },
  data(){
    return {
      subreddit: 'ProgrammerHumor',
      posts: [],
      favouriteSubreddits: []
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
      addToFavourites: function(){
        if (this.favouriteSubreddits.filter(item => this.subreddit === item).length === 0){
        this.favouriteSubreddits.push(this.subreddit)}
      }
        
    },
}
</script>

<style>
body{
  background-color: black;
}
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
