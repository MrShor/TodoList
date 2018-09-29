<template>
  <div>
    <legend class="header">Todo here!</legend>
    <input type="text" class="todo-input" placeholder="What need to be done" v-model="newTodo" @keyup.enter="addTodo"> 
    <!-- @keyup.enter="addTodo" ==> methodos: {addTodo(){alert('adding')}} -->
    <div v-for="todo in todos" :key="todo.id" class="todo-item">
      {{ todo.title }}
    </div>
  </div>
</template>

<script>
export default {
  name: 'todo-list', //What this???
  data () {
    return {
      newTodo: '',
      idForTodo: 3,
      todos: [
        {
          'id': 1,
          title: 'Finish Vue Screencst',
          'completed':false,
        },
        {
          'id': 2,
          title: 'Take over world',
          'completed':false,
        },
      ]
    }
  },
  methods: {
    addTodo() {
      // alert('adding')  //Real Working!
      this.todos.push({
        id: this.idForTodo,
        title: this.newTodo,
        completed: false,
      })
      this.newTodo = ''
      this.idForTodo++
    }
  }
}
</script>


<style lang="scss">
.header {
  text-align: center;
  margin: 16px;
  // paddin g: 16px;
}
  .todo-input {
    width: 100%;
    padding: 10px 18px;
    font-size: 18px;
    margin-bottom: 16px;
    &:focus {
      outline: 0;
    }
  }
</style>
