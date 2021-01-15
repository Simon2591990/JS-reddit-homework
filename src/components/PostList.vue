<template lang="html">
  <div>
      <div v-for="post in postList">
        <h2 v-on:click="selectPost(post)">{{post.data.title}}</h2>
        <img v-if="selectedPost === post" :src="post.data.thumbnail">
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
            selectedPost: null
        }
        
    },
    methods:{
        selectPost: function(post){
            this.selectedPost = post

        }    
    }
}

</script>

<style>

</style>