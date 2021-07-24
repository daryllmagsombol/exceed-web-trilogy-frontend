<template>
  <div class="container">
    <ComposePost 
      @add-post="addPost($event)"
    />
    <Posts 
      :posts="posts" 
      @delete-post="deletePost($event)"
      @edit-post="editPost($event)"   
    />
  </div>
</template>

<script>
import ComposePost from './components/ComposePost.vue'
import Posts from './components/Posts.vue';

export default {
  name: 'App',
  components: {
    ComposePost,
    Posts
  },
  data () {
    return{
      baseUrl: process.env.VUE_APP_BASE_URL + process.env.VUE_APP_API_VERSION,
      posts: []
    }
  },
  methods: {
    async getPosts(){
      const res = await fetch(this.baseUrl + '/posts', {
        method: 'GET',
      });
      const data = await res.json();
      this.posts = data;
    },

    async addPost(post){
      const res = await fetch(this.baseUrl + '/posts', {
        method: 'POST',
        headers: {
          'Content-type': 'Application/json',
        },
        body: JSON.stringify(post)
      });
      const responseData = await res.json();
      this.posts.push(responseData);
    },

    async deletePost(post){
      const res = await fetch(`${this.baseUrl}/posts/${post.id}`, {method: 'DELETE'});
      const data = await res.json();
      this.posts.splice(this.posts.indexOf(post), 1);
      alert(data.message);
    },

    async editPost(post){
      const res = await fetch(`${this.baseUrl}/posts/${post.id}`, {
        method: 'PATCH',
        headers: {
          'Content-type': 'Application/json'
        },
        body: JSON.stringify(post)
      });
      const data = await res.json();
      if(data){
        await this.getPosts();
      }
    }

  },
  async created(){
     this.getPosts();
  }
}
</script>

<style>

</style>
