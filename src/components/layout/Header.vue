<template>
    <header class="todo-list-header">
        <div>
            <h3>{{timestamp}}</h3>
        </div>
        <div class="todo-list-header-main">
            <h1>Your Tasks</h1>
        </div>
    </header>
</template>

<script>
  export default {
    name: 'Header',
    data () {
      return {
        timestamp: new Date().toDateString()
      }
    }
  }
</script>

<style scoped>
    .todo-list-header {
        background-image: url("../../assets/headerBackground.jpg");
        background-size: cover;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        height: 150px;
        padding: 5px;
        color: #fff;
    }

    .todo-list-header-main {
        text-align: end;
        margin-bottom: 25px;
    }

    h1, h3 {
        font-weight: lighter;
    }
</style>