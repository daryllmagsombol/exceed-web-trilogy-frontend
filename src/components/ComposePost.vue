<template>
  <div class="card my-3 animate__animated animate__fadeIn border-0 shadow rounded-0">
    <div class="card-header">
      <p class="h3">Create Post</p>
    </div>

    <div class="card-body p-3s">
      <form @submit="onSubmit">

        <div class="form-group mb-3">
          <label for="">Author *</label>
          <input class="form-control rounded-0" v-model="author" type="text">
        </div>

        <div class="form-group mb-3">
          <label for="">Title *</label>
          <input class="form-control rounded-0" v-model="title" type="text">
        </div>
        <div class="form-group mb-3">
          <label for="">Body *</label>
          <textarea class="form-control rounded-0" v-model="body" rows="5"></textarea>
        </div>

        <div class="d-grid mt-4">
          <input type="submit" value="Post" class="btn btn-info text-light btn-block">
        </div>
      </form>
    </div>
  
  </div>

</template>

<script>
export default {
  name: 'ComposePost',
  data() {
    return{
      author: null,
      title: null,
      body: null,
    }
  },
  methods: {
    onSubmit(e){
      e.preventDefault();
      if(!this.author || !this.title || !this.body){
        alert('Required fields cannot be empty');
        return;
      }
      let post = {
        author: this.author,
        title: this.title,
        body: this.body
      };
      this.$emit('add-post', post);
      this.resetFields();
    },
    resetFields(){
      this.author = null;
      this.title = null;
      this.body = null;
    }
  }
}
</script>

<style scoped>
  label{
    font-size: 13px;
    margin-bottom: 0.5rem;
  }
</style>
