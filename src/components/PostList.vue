<template lang="html">
  <div>
    <div id="post"  v-for="post in postList" v-if="!post.data.is_video">
        <post-details :postDetails="post"></post-details>
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
    }
     
        // fetch post.data.permalink to display comments
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