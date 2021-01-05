<template>
  <div>
    <h1>Comment system</h1>
    <hr />
    <FormTodo v-on:add-todo="addComment"/>
    <div class="list-group">
      <div class="list-group-item" v-for="(comment, index) in allComments" :key="index.id">
        <span class="comment_author">
          Author: <strong>{{ comment.name }}</strong>
        </span>
        <p>{{ comment.message }}</p>
        <div>
          <a href="#" title="Delete" v-on:click.prevent="removeComment(index)">Delete</a>
        </div>
      </div>
    </div>
  </div>
</template>


<script>
  import FormTodo from './FormTodo'
  export default {
    components: {
      FormTodo
    },
    data() {
      return {
        comments: [],
      }
    },
    methods: {
      addComment(comment) {
        this.comments.push(comment);
      },
      removeComment(index){
        this.comments.splice(index, 1);
      }
    },
    computed: {
      allComments () {
          return this.comments.map(comment => ({
            ...comment,
            name: comment.name.trim() === '' ? 'Anonymous' : comment.name
          }))
        }
    },
    watch: {
      comments(val) {
        console.log('val', val)
      }
    }
  }
</script>
