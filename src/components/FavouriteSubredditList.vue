<template lang="html">
  <div> 
      <h2>Favourite Subreddits</h2>
    <select v-on:change="changeSubreddit">
        <option v-for="subreddit in favouritesList">{{subreddit}}</option>
    </select>
  </div>
</template>

<script>
import {eventBus} from "@/main"
export default {
    name: "favourite-subreddits",
    props: ["favouritesList"],
    methods:{
        changeSubreddit: function(){
            eventBus.$emit("subreddit", event.target.value)            
        }
    }

}
</script>

<style>

</style>