<template>
    <div class="todo-item" v-bind:class="{'is-complete':todo.completed}">
        <div class="todo-title-container">
            <div class="todo-title-label" v-if="!todo.editing" @dblclick="editTodo(todo)">{{todo.title}}</div>
            <input v-else class="todo-title-input" type="text" v-model="todo.title" @blur="doneEdit(todo)"
                    @keyup.enter="doneEdit(todo)" @keyup.esc="cancelEdit(todo)" v-focus>
        </div>
        <div class="checkbox-container circular-container">
            <label class="checkbox-label">
                <input class="todo-item-mark-complete" type="checkbox" v-on:change="markComplete">
                <span class="checkbox-custom circular" />
            </label>
            <button class="todo-item-delete" @click="$emit('del-todo', todo.id)">
                <i class="fa fa-trash-o fa-lg" />
            </button>
        </div>
    </div>
</template>

<script>
  export default {
    name: "TodoItem",
    props: ["todo"],
    directives: {
      focus: {
        inserted: function (el) {
          el.focus()
        }
      }
    },
    methods: {
      markComplete () {
        this.todo.completed = !this.todo.completed
      },
      editTodo (todo) {
        this.beforeEdit = todo.title
        todo.editing = true
      },
      doneEdit (todo) {
        if (todo.title === '') {
          todo.title = this.beforeEdit
        }
        todo.editing = false
      },
      cancelEdit (todo) {
        todo.title = this.beforeEdit
        todo.editing = false
      }
    }
  }
</script>

<style scoped>
    .todo-title-container {
        flex-grow: 1;
    }

    .todo-title-input, .todo-title-label {
        display: block;
        width: 100%;
        line-height: 21px;
        font-size: 18px;
        margin-block-start: 1em;
        margin-block-end: 1em;
        margin-inline-start: 0px;
        margin-inline-end: 0px;
        font-weight: lighter;
        border: none;
        margin: 0;
        padding: 0;
        outline: none;
        background-color: transparent;
    }

    .todo-title-input {
        border: 1px solid grey;
        margin: 2px;
        padding: 7px 2px;
    }

    .todo-title-label {
        padding: 10px 5px;
    }

    .todo-title-input {
        color: grey;
    }

    .todo-item {
        display: flex;
        justify-content: space-between;
        align-items: center;
        background-color: #fff;
        border-bottom: 1px solid darkgrey;
        border-left: 1px solid darkgrey;
        border-right: 1px solid darkgrey;
    }

    .todo-item.is-complete {
        background-color: darkgrey;
    }

    .todo-item.is-complete div {
        text-decoration: line-through;
    }

    .checkbox-container.circular-container {
        display: flex;
    }

    .checkbox-label {
        display: block;
        position: relative;
        margin: 0 10px;
        cursor: pointer;
        height: 22px;
        width: 22px;
    }

    .checkbox-label input {
        position: absolute;
        opacity: 0;
        cursor: pointer;
    }

    .checkbox-label .checkbox-custom {
        position: absolute;
        top: 0px;
        left: 0px;
        height: 22px;
        width: 22px;
        background-color: transparent;
        transition: all 0.3s ease-out;
        -webkit-transition: all 0.3s ease-out;
        -moz-transition: all 0.3s ease-out;
        -ms-transition: all 0.3s ease-out;
        -o-transition: all 0.3s ease-out;
    }

    .checkbox-label .checkbox-custom::after {
        position: absolute;
        content: "";
        left: 12px;
        top: 12px;
        height: 0px;
        width: 0px;
        -webkit-transform: rotate(0deg) scale(0);
        -ms-transform: rotate(0deg) scale(0);
        transform: rotate(0deg) scale(0);
        transition: all 0.3s ease-out;
        -webkit-transition: all 0.3s ease-out;
        -moz-transition: all 0.3s ease-out;
        -ms-transition: all 0.3s ease-out;
        -o-transition: all 0.3s ease-out;
    }

    .is-complete .checkbox-label .checkbox-custom::after {
        -webkit-transform: rotate(45deg) scale(1);
        -ms-transform: rotate(45deg) scale(1);
        transform: rotate(45deg) scale(1);
        left: 7px;
        top: 3px;
        width: 5px;
        height: 10px;
    }

    .checkbox-label .checkbox-custom::before {
        position: absolute;
        content: "";
        left: 10px;
        top: 10px;
        width: 0px;
        height: 0px;
        -webkit-transform: scale(0);
        -ms-transform: scale(0);
        transform: scale(0);
    }

    .is-complete .checkbox-label .checkbox-custom::before {
        left: 3px;
        top: 3px;
        width: 12px;
        height: 12px;
        -webkit-transform: scale(3);
        -ms-transform: scale(3);
        transform: scale(3);
        opacity: 0;
        z-index: 999;
        transition: all 0.3s ease-out;
        -webkit-transition: all 0.3s ease-out;
        -moz-transition: all 0.3s ease-out;
        -ms-transition: all 0.3s ease-out;
        -o-transition: all 0.3s ease-out;
    }

    .checkbox-label .checkbox-custom.circular {
        border-radius: 50%;
        border: 1px solid grey;
    }

    .is-complete .checkbox-label .checkbox-custom.circular {
        background-color: #fff;
        border-radius: 50%;
        border: 1px solid grey;
    }

    .is-complete .checkbox-label .checkbox-custom.circular::after {
        border: solid #0067ff;
        border-width: 0 2px 2px 0;
    }

    .checkbox-label .checkbox-custom.circular::before {
        border-radius: 50%;
        border: 1px solid #0067ff;
    }

    .is-complete .checkbox-label .checkbox-custom.circular::before {
        border-radius: 50%;
    }

    .todo-item-delete {
        height: 22px;
        width: 22px;
        margin-right: 5px;
        background-color: #ed2939;
        border-radius: 50%;
        border: 1px solid #ed2939;
        color: #fff;
        cursor: pointer;
        transition: background-color 0.4s, border-color 0.4s;
        overflow: hidden;
        outline: none;
    }

    .todo-item-delete:hover {
        background-color: #960018;
        border-color: #960018;
    }

    .todo-item-delete i {
        font-size: 16px;
    }
</style>