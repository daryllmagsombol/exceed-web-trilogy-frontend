<template> 
    <div >
        <div v-if="!isEditing" class="card animate__animated animate__fadeIn">
            <div class="card-header">
                <p class="h3 post-title" v-if="!isEditing">{{post.title}}</p>
                <div class="actions">
                    <button class="btn btn-danger btn-sm" @click="deletePost()">Delete</button>
                    <button class="btn btn-info text-light btn-sm ms-1" @click="toggleEdit()">Edit</button>
                </div>
            </div>
            <div class="card-body">
                <p class="post-body">{{post.body}}</p>
            </div>
            <div class="card-footer">
                <p class="post-author">By: <span class="author">{{post.author}}</span> - {{post.createdAt}}</p>
            </div>
        </div>

        <div v-if="isEditing" class="card animate__animated animate__fadeIn">
            <div class="card-header">
                <div class="form-group" v-if="isEditing">
                    <input class="form-control" type="text" v-model="editedPost.title">
                </div>
                <div class="actions">
                    <button class="btn btn-success btn-sm" @click="editPost()">Save</button>
                    <button class="btn btn-info text-light btn-sm ms-1" @click="toggleEdit()">Cancel</button>
                </div>
            </div>
            <div class="card-body p-2">
                <textarea class="form-control" v-model="editedPost.body" rows="5"></textarea>
            </div>
            <div class="card-footer">
                <p class="post-author">By: <span class="author">{{post.author}}</span> - {{post.createdAt}}</p>
            </div>
        </div>

    </div>
</template>

<script>

export default {
  name: 'Post',
  data() {
      return{ 
        isEditing: false,
        editedPost: {}
      }
  },
  props: {
    post: {}
  },
  methods: {
    deletePost(){
        if(confirm('Do you want to delete this post?')){
            this.$emit('delete-post',this.post);
        }
    },
    toggleEdit(){
        this.isEditing = !this.isEditing;
        Object.assign(this.editedPost, this.post);
    },
    editPost(){

        if(!this.editedPost.author || !this.editedPost.title || !this.editedPost.body){
        alert('Required fields cannot be empty');
        return;
      }

        if(confirm('Do you want to edit this post?')){
            this.$emit('edit-post',this.editedPost);
            this.isEditing = false;
        }
    }
  }
}
</script>

<style scoped>

    .card{
        border: 0;
        box-shadow: 0 .5rem 1rem rgba(0,0,0,.15);
        border-radius: 0;
    }

    .card-header{
        padding: 1.5rem 1rem;
        display: flex;
        align-items: center;
        gap: 1em;
    }

    .card-header .form-group{
        flex-grow: 1;
    }

    .card-header .actions{
        margin-left: auto;
    }

    .post-title{
        color: #000000;
        margin: 0;
    }
    
    .card-body{
        padding: 1.5rem 1rem;
    }

    .post-body{
        font-size: 13px;
    }

    .form-control{
        border-radius: 0;
    }

    .post-author{
        margin: 0;
        font-size: 12px;
        font-style: italic;
    }

    .post-author .author{
        font-weight: bold;
    }

</style>
