<template>
  <div v-if="thread" class="col-large push-top">
    <h1>{{ thread.title }}</h1>

    <post-list :posts="threadPosts" />
  </div>
  <div v-else class="col-full text-center">
    <h1>This thread does not exist</h1>
    <router-link :to="{ name: 'Home' }">Read some cool threat</router-link>
  </div>
</template>

<script>
import sourceData from '@/data.json'
import PostList from '@/components/PostList'

export default {
  name: 'ThreadShow',
  components: {
    PostList
  },
  props: {
    id: {
      required: true,
      type: String
    }
  },
  data () {
    return {
      threads: sourceData.threads,
      posts: sourceData.posts
    }
  },
  computed: {
    threadPosts () {
      return this.posts.filter((post) => post.threadId === this.id)
    },
    thread () {
      return this.threads.find((thread) => thread.id === this.id) // also available under this.$route.params.id
    }
  }
}
</script>
