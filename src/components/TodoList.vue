<template>
  <div>
    <legend class="header">Todo here!</legend>
    <!-- @keyup.enter="addTodo" ==> methodos: {addTodo(){alert('adding')}} -->
    <input type="text" class="todo-input" placeholder="What need to be done" v-model="newTodo" @keyup.enter="addTodo"> 
    <div v-for="(todo, index) in todos" :key="todo.id" class="todo-item">
      <div class="todo-item-left">
        <input type="checkbox" v-model="todo.completed">
        <div v-if="!todo.editing" @dblclick="editTodo(todo)" class="todo-item-label" :class="{ completed : todo.completed }">{{ todo.title }}</div>

        <input v-else="" class="todo-item-edit" type="text" v-model="todo.title" @blur="doneEdit(todo)" @keyup.enter="doneEdit(todo)" @keyup.esc="cancelEdit(todo)" v-focus>
      </div>

      <div class="remove-item" @click="removeTodo(index)">
        &times;
      </div>
    </div>

    <div class="extra-container">
      <div><label><input type="checkbox" :checked="!anyReamining" @change="checkAllTodos">Check All </label></div>
      <div>{{ reamining }} items left</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'todo-list', //What this???
  // Were is Bugs???? ===>>>
  data () {
    return {
      newTodo: '',
      idForTodo: 3,
      beforeEditCache: '',
      todos: [
        {
          'id': 1,
          title: 'Finish Vue Screencst',
          'completed':false,
          'editing': false,
        },
        {
          'id': 2,
          title: 'Take over world',
          'completed':false,
          'editing': false
        },
      ]
    }
  },
  // <<<=== He is here???
  computed: {
    reamining() {
      return this.todos.filter(todo => !todo.completed).length
    },
    anyReamining() {
      return this.reamining != 0
    }
  },
  directives: { //For work focus-dblclick + v-focus
    focus: {
      inserted: function (el) {
        el.focus()
      }
    }
  },
  methods: {
    addTodo() {
      // alert('adding')  //Real Working!
      if(this.newTodo.trim().length == 0) {
        return
      }
      this.todos.push({
        id: this.idForTodo,
        title: this.newTodo,
        completed: false,
      })
      this.newTodo = ''
      this.idForTodo++
    },
    editTodo(todo) {
      alert ('double clicked')
      this.beforeEditCache = todo.title
      todo.editing = true
    },
    doneEdit(todo) {
      if (todo.title.trim() == '') {
        todo.title = this.beforeEditCache
      }
      todo.editing = false
    },
    cancelEdit(todo) {
      todo.title = this.beforeEditCache
      todo.editing = false
    },
    removeTodo(index) {
      this.todos.splice(index, 1)
    },
    checkAllTodos() {
      this.todos.forEach((todo) => todo.completed = event.target.checked)
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
  .todo-item {
    margin-bottom: 12px;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  .remove-item {
    cursor: pointer;
    margin-left: 14px;
    &:hover {
      color:red;
    }
  }
  .todo-item-left {
    display: flex;
    align-items: center;
  }
  .todo-item-label {
    padding: 10px;
    border: 1px solid white;
    margin-left: 12px;
  }
  .todo-item-edit {
    font-size: 24px;
    color: #2c3e50;
    margin-left: 12px;
    width: 100%;
    padding: 10px;
    border: 1px solid #ccc; 
    font-family: 'Avenir', Helvetica, Arial, Helvetica, sans-serif;

    &focus {
      outline: none;
    }
  }
  .completed {
    // Working whith + :class="{ completed : todo.completed }
    text-decoration: line-through;
    color: green;
  }

  .extra-container {
    display: flex;
    align-items: center;
    justify-content: space-between;
    font-size: 16px;
    border-top: 1px solid lightgray;
    padding-top: 14px;
    margin-bottom: 14px;
  }
  button {
    font-size: 14px;
    background-color: red;
    appearance: none;
    &:hover {
      background: lightgreen;
    }
    &:focus {
      outline: none
    }
  }
  .active {
    background: lightgreen;
  }
</style>