<script setup>
  import {ref, computed, onMounted} from 'vue'


  import ButtonCounter from './components/ButtonCounter.vue'
  import BlogPost from './components/BlogPost.vue';
  import PaginatePost from './components/PaginatePost.vue'
  import LoadingSpinner from './components/LoadingSpinner.vue'

  const posts = ref([])

  const favorite = ref('')

  const changeFavorite = (post) => {
    favorite.value = post
  }

  const postXPage = 20

  let first = ref(0)
  let last = ref(postXPage)

  let loading = ref(true)

  const next = () => {
    first.value += postXPage
    last.value += postXPage
  }

  const previous = () => {
    first.value -= postXPage
    last.value -= postXPage
  }

  onMounted(async() => {



  })

  const fetchData = async () => {
    try {
      const res = await fetch('https://jsonplaceholder.typicode.com/posts')
      posts.value = await res.json()
    } catch(error) {
      console.log(error)
    } finally {

      setTimeout(() => loading.value = false, 1500)
      
    }
  }

  fetchData()

  // fetch('https://jsonplaceholder.typicode.com/posts')
  // .then(res => res.json())
  // .then(data => {
  //   posts.value = data
  //   console.log(data)
  // })
  // .catch(err => console.error(err))
  // .finally( () => {
  //   setTimeout(() => loading.value = false, 1500)
  //   console.log(loading)
  // })

  const numberOfPosts = computed( () => posts.value.length)

</script>

<template>

  <LoadingSpinner v-if="loading">

  </LoadingSpinner>

  <div class="container" v-else>
    <h1>APP</h1>
    <!-- <ButtonCounter></ButtonCounter> -->
    <h5>My favorite post: {{ favorite }}</h5>

    <PaginatePost 
      :first="first"
      :last="last"
      :numberOfPosts="numberOfPosts"
      @next="next"
      @previous="previous"
      class="mb-2">

    </PaginatePost>

    <BlogPost v-for="post in posts.slice(first, last)" :key="post.id" 
        :id="post.id"
        :title="post.title"
        :content="post.body"
        @changeFavorite="changeFavorite"
        class="mb-2">
    </BlogPost>
    
  </div>

</template>

<style>
</style>