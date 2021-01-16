<template lang="html">
  <div> 
      <h2>Favourite Subreddits</h2>
    <select>
        <option v-for="subreddit in favouritesList">{{subreddit}}</option>
    </select>
  </div>
</template>

<script>
export default {
    name: "favourite-subreddits",
    props: ["favouritesList"]

}
</script>

<style>

</style>