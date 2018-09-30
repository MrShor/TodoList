<template>
  <div id="app" class="container">
    <img src="./assets/logo.png" class="logo">
    <!-- this components off to choose from -->
    <!-- <HelloWorld/> -->
    <!-- <hello-world></hello-world> -->
    <TodoList/>
    <!-- <todo-list/> -->
    <!-- Equivalent, Why??? -->
    <!-- <hello-world></hello-world> </hello-world> <HelloWorld/>-->
    <!-- <todo-list></todo-list> === <todo-list/> === <TodoList/> -->
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorldOld'
import TodoList from './components/TodoList'
export default {
  name: 'App',
  components: {
    HelloWorld,
    TodoList,
  }
}
</script>

<style>
* {
  box-sizing: border-box;
}
.container {
  max-width: 600px;
  margin: 0 auto;
}
.logo {
  display: block;
  margin: 20px auto;
  height: 100px;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
  margin-top: 60px;
  font-size: 24px;
}
</style>