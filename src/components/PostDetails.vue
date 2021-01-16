<template lang="html">
  <div>
      <h2 v-on:click="selectPost(postDetails)">{{postDetails.data.title}}</h2>
        <img v-on:click="unSelectPost(postDetails)" id="image" v-if="selectedPost === postDetails && !postDetails.data.is_self" :src="postDetails.data.url">
        <img v-on:click="selectPost(postDetails)" id="thumbnail" v-if="!postDetails.data.is_self && postDetails !== selectedPost" :src="postDetails.data.thumbnail">
        <h3 v-if="postDetails.data.is_self" v-on:click="selectPost(postDetails)">Text Post</h3>
        <p v-on:click="unSelectPost(post)" v-if="postDetails.data.is_self && postDetails === selectedPost" >{{postDetails.data.selftext}}</p> 
      <p>Posted by {{postDetails.data.author}}</p>
        <button v-on:click="savePost">Save</button>
  </div>
</template>

<script>
import {eventBus} from "@/main"

export default {
    name: 'post-details',
    props: ['postDetails'],
    data(){
        return{
            selectedPost: ""
        }
    },
    methods:{
        selectPost: function(post){
            this.selectedPost = post
        },
        unSelectPost: function(post){
            this.selectedPost = null
        }, 
        savePost: function(){
            eventBus.$emit('savedPost', this.postDetails )
        }
    }
    
}
</script>

<style>

</style>