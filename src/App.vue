<template>
  <h1>Vue 3 Todo App</h1>
  <form @submit.prevent="addNewTodo">
    <label>New Todo</label>
    <input v-model="newTodo" name="newTodo">
    <button>Add New Todo</button>
  </form>
  <button @click="removeAllTodos">Remove All</button>
  <button @click="markAllDone">Mark All Done</button>
  <ul>

  </ul>
    <li v-for="todo in todos" :key="todo.id" class="todo">
        <h3 :class="{ done: todo.done}" @click="toogleDone(todo)">{{todo.content}}</h3>
        <button @click="removeTodo(index)">Remove Todo</button>
    </li>
</template>


<script>
import { ref } from 'vue';

export default {
    setup(){
        const newTodo =  ref('');
        const todos = ref([]);

        function addNewTodo(){
            todos.value.push({
                id:Date.now(),
                done:false,
                content:newTodo.value,
            });
            newTodo.value = '';
        }
        function toogleDone(todo){
            todo.done = !todo.done;
        }

        function removeTodo(index) {
            todos.value.splice(index, 1);
        }
        function markAllDone() {
            todos.value.forEach((todo) => todo.done = true);
        }

        function removeAllTodos(){
            todos.value =[];
        }

        return {
            todos,
            newTodo,
            addNewTodo,
            toogleDone,
            removeTodo,
            markAllDone,
            removeAllTodos,
        };

    }
}
</script>

<style scoped>
body {
  font-family: sans-serif;
  padding-top: 1em;
  padding-bottom: 1em;
  font-size: 2em;
  width: 80%;
  margin: 0 auto;
}
 textarea, button, p, div, section, article, select {
  display: 'block';
  width: 90%;
  font-family: sans-serif;
  font-size: 1em;
  margin: 1.5em;
  cursor: pointer;
  padding: 10px;
  display: flex;
  justify-content: center;
}
input{
    width: 88%;
    font-family: sans-serif;
    font-size: 1em;
    margin: 1.5em;
    cursor: pointer;
    padding: 10px;
    display: flex;
    justify-content: center;
}

.todo {
  cursor: pointer;
}

.done {
  text-decoration: line-through;
}
</style>
