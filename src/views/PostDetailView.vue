<template>
  <div class="post-detail">
    <h1>This is a post</h1>
    <p>Display the content of post with ID of {{$route.params.id}} here!</p>
    <div>
      <button @click="showPostId">Show post ID</button>
    </div>
    <div>
      <button @click="goHomeIn3Seconds">Go home in 3 seconds</button>
    </div>

    <p><RouterLink to="/posts">&lt; Back</RouterLink> </p>
  </div>
</template>

<script setup>
import { useRoute, useRouter } from 'vue-router';

const route = useRoute() 
const router = useRouter() 

const showPostId = () => {
  alert(`The ID of this post is: ${ route.params.id} `)
}

const goHomeIn3Seconds = () => {
  setTimeout(() => {
router.push('/')
  }, 3000)
}
</script>