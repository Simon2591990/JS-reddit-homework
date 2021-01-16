<template lang="html">
  <div id="app">
    <h1>Reddit App</h1>
    <button v-on:click="changePage('posts')"> All Posts</button>
    <button v-on:click="changePage('saved')">Saved</button>
    <div v-if="page == 'posts'">
      <h1 v-if="posts">{{posts[0].data.subreddit_name_prefixed}}</h1>
      <form v-on:submit.prevent="getPosts">
      <input type="text" v-model="subreddit">
      <button type="submit">Go</button><br>
      <button v-on:click="addToFavourites">Add Subreddit to Favourites</button>
      <favourite-subreddits v-if="favouriteSubreddits.length > 0" :favouritesList="favouriteSubreddits"></favourite-subreddits>
      <button v-if="favouriteSubreddits.length > 0"  type="submit">Go</button>
      </form>
      <post-list :postList="posts"></post-list>
    </div>
        
  </div>
</template>

<script>
import PostList from './components/PostList.vue'
import FavouriteSubredditList from './components/FavouriteSubredditList.vue'
import {eventBus} from "@/main"


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
      favouriteSubreddits: [],
      page: ''

    }
  },
    mounted(){
      this.getPosts() 
      eventBus.$on("subreddit", subreddit => this.subreddit = subreddit)
      this.getPosts() 
      

    },
  methods:{
      getPosts: function(){
        fetch(`https://www.reddit.com/r/${this.subreddit}.json`)
        .then(res => res.json())
        .then(allData => this.posts = allData.data.children)
      },
      addToFavourites: function(){
        if (this.favouriteSubreddits.filter(item => this.subreddit === item).length === 0){
        this.favouriteSubreddits.push(this.subreddit)}
      },
      changePage: function(page){
        this.page = page
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
button{
  background-color: black;
  color: white;
  border: 1px solid rgb(32, 32, 32);
  padding: 10px
}

</style>
