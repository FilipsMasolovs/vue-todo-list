<template>
    <div id="app">
        <Header />
        <div class='list-select'>
            <button :class="{ active: filter == 'all' }" @click="filter = 'all'">All</button>
            <button :class="{ active: filter == 'active' }" @click="filter = 'active'">Active</button>
            <button :class="{ active: filter == 'completed' }" @click="filter = 'completed'">
                Completed
            </button>
        </div>
        <Todos v-bind:todosFiltered="todosFiltered" v-on:del-todo="deleteTodo" />
        <AddTodo v-on:add-todo="addTodo" />
    </div>
</template>

<script>
  import Header from './components/layout/Header';
  import AddTodo from './components/AddTodo';
  import Todos from './components/Todos';

  export default {
    name: 'App',
    components: {
      Header,
      Todos,
      AddTodo
    },
    data () {
      return {
        filter: 'all',
        todos: [
          {
            id: 1,
            title: 'Become React sensei',
            completed: false,
            editing: false
          },
          {
            id: 2,
            title: 'Become Vue.js master',
            completed: false,
            editing: false
          },
          {
            id: 3,
            title: 'Win McJohn in chess',
            completed: true,
            editing: false
          },
          {
            id: 4,
            title: 'Save up 4000 EUR',
            completed: false,
            editing: false
          },
          {
            id: 5,
            title: 'Get a good job',
            completed: true,
            editing: false
          },
          {
            id: 6,
            title: 'Finish this ToDo app',
            completed: false,
            editing: false
          }
        ],
        beforeEdit: ''
      }
    },
    computed: {
      todosFiltered () {
        if (this.filter == 'all') {
          return this.todos
        } else if (this.filter == 'active') {
          return this.todos.filter(todo => !todo.completed)
        } else if (this.filter == 'completed') {
          return this.todos.filter(todo => todo.completed)
        }
        return this.todos
      }
    },
    methods: {
      deleteTodo (id) {
        this.todos = this.todos.filter(todo => todo.id !== id)
      },
      addTodo (newTodo) {
        this.todos = [...this.todos, newTodo]
      }
    }
  }
</script>

<style>
    @import url('https://fonts.googleapis.com/css?family=Roboto:400,500,700&display=swap');

    * {
        box-sizing: border-box;
        margin: 0;
        padding: 0;
    }

    body {
        font-family: ‘Roboto’, sans-serif;
        -webkit-font-smoothing: antialiased;
        line-height: 1;
        display: flex;
        justify-content: center;
        align-items: center;
        width: 100vw;
        height: 100vh;
        background-color: #63a4ff;
        background-image: linear-gradient(315deg, #63a4ff 0%, #83eaf1 74%);
    }

    #app .list-select {
        position: absolute;
        top: 120px;
        right: 5px;
    }

    #app .list-select button {
        padding: 5px;
        margin: 5px 2px -5px;
        border-top-left-radius: 5px;
        border-top-right-radius: 5px;
        border-color: darkgrey;
        outline: none;
        cursor: pointer;
        transition: background-color 0.4s;
    }

    #app .list-select button:hover {
        background-color: darkgrey;
    }

    #app {
        width: 100%;
        max-width: 400px;
        position: relative;
    }
</style>
