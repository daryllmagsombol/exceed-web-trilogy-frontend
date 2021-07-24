<template> 
    <div>
        <div v-for="post in posts" :key="post.id"  class="my-3">
          <Post 
            :post="post" 
            @delete-post="deletePost($event)"
            @edit-post="editPost($event)"
          />
        </div>
    </div>
</template>

<script>
import Post from './Post.vue';

export default {
  name: 'Posts',
  props: {
    posts: [],
  },
  components: {
    Post
  },
  methods: {
    deletePost(post){
      this.$emit('delete-post', post);
    },
    editPost(post){
      this.$emit('edit-post', post);
    }
  }
}
</script>

<style scoped>
</style>
