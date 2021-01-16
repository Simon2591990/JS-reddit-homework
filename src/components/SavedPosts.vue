<template>
    <div>
         <h1>This is the saved posts page</h1>
         <li v-for="post in savedPosts">{{post.data.title}}</li>
    </div>
    
</template>

<script>


export default {
    name: "saved-posts",
    props: ['savedPosts'],
}
</script>

<style>

</style>