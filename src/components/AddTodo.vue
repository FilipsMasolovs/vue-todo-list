<template>
    <div>
        <form class="add-todo-form" @submit="addTodo">
            <input class="add-todo-input" type="text" name="title" v-model="title" placeholder="Add Todo...">
            <button class="add-todo-button" type="submit">
                <i class="fa fa-plus fa-lg" />
            </button>
        </form>
    </div>
</template>

<script>
  export default {
    name: "AddTodo",
    data () {
      return {
        title: ''
      }
    },
    methods: {
      addTodo (e) {
        if (this.title === '') {
          e.preventDefault();
        } else {
          e.preventDefault();
          const newTodo = {
            id: 'id-' + this.title + '-added-on-' + new Date(),
            title: this.title,
            completed: false
          }
          this.$emit('add-todo', newTodo);
          this.title = '';
        }
      }
    }
  }
</script>

<style scoped>
    .add-todo-form {
        display: flex;
        padding: 10px 5px;
        border-bottom: 1px solid darkgrey;
        border-left: 1px solid darkgrey;
        border-right: 1px solid darkgrey;
        border-bottom-left-radius: 10px;
        border-bottom-right-radius: 10px;
        background-color: #fff;
    }

    .add-todo-input {
        flex-grow: 1;
        font-size: 1.17em;
        border: none;
        outline: none;
    }

    .add-todo-button {
        height: 22px;
        width: 22px;
        margin-left: 10px;
        background-color: #028a0f;
        border-radius: 50%;
        border: 1px solid #028a0f;
        color: #fff;
        cursor: pointer;
        transition: background-color 0.4s, border-color 0.4s;
        outline: none;
    }

    .add-todo-button:hover {
        background-color: #234f1e;
        border-color: #234f1e;
    }

    .add-todo-button i {
        font-size: 16px;
    }
</style>