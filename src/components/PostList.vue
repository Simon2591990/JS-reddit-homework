<template lang="html">
  <div>
      <div id="post"  v-for="post in postList" v-if="!post.data.is_video">
        <h2 v-on:click="selectPost(post)">{{post.data.title}}</h2>
        <img v-on:click="unSelectPost(post)" id="image" v-if="selectedPost === post && !post.data.is_self" :src="post.data.url">
        <!-- <img v-on:click="selectPost(post)"id="thumbnail"  :src="post.data.thumbnail"> -->
        <img v-on:click="selectPost(post)"id="thumbnail" v-if="!post.data.is_self && post !== selectedPost" :src="post.data.thumbnail">
        <h3 v-if="post.data.is_self">Text Post</h3>
        <p v-on:click="unSelectPost(post)" v-if="post.data.is_self && post === selectedPost" >{{post.data.selftext}}</p>
        </div>
  </div>
</template>

<script>
import PostDetails from './PostDetails.vue'
export default {
    name: 'post-list',
    props: ['postList'],
    components: {
        'post-details': PostDetails
    },
    mounted(){
    },
    data(){
        return{
            selectedPost: null,
        }
    
        
    },
    methods:{
        selectPost: function(post){
            this.selectedPost = post
        },
        unSelectPost: function(post){
            this.selectedPost = null
        },  
        // fetch post.data.permalink to display comments
    }
}

</script>

<style>
#thumbnail{
    width: 50px
}
#image{
    width: 500px
}
#post{
    background-color: rgb(16, 16, 16);
}
#black{
    background-color: rgb(0, 0, 0);
}

</style>