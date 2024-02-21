<script setup>
const msg = 'To do App';
import {ref, onMounted, watch} from "vue";

const todos = ref([]);
const text = ref("");
function addTodo() {
  if (text.value.trim() === "") {
    return;
  }

  todos.value.unshift({
    todo: text.value,
    done: false,
  });

  text.value = "";
}

function deleteTodo(todo) {
  todos.value = todos.value.filter((x) => x !== todo);
} 
watch(
 todos,
  (newTodoValue) => {
    localStorage.setItem("todos", JSON.stringify(newTodoValue));
  },
  { deep: true }
);
onMounted(() => {
  todos.value = JSON.parse(localStorage.getItem("todos")) || [];
});
</script>

<template>

  
 <main class="app">
    <section class="greeting">
      <h1 class="title" >ToDo App
          
        
      </h1>
     
    </section>
    <div class="input-section">
      <section class="create-todo">
        <form @submit.prevent="addTodo">
          <h2>please add to do?</h2>
           
          <input
            type="text"
            placeholder="tell Liam his dogs cute"
            v-model="text"
          />
          <input type="submit" value="Add todo" />
        </form>
      </section>
    </div>
   <div class="todo-section">
    <section class="todo-list">
      <h3 v-show="todos.length=== 0">No ToDos currently active</h3>
      <div class="list">

      <div
      v-for="todo in todos"
       class="todo-item $ {todo.done && 'done'}"
      >
      <label>
        <input type="checkbox" v-model="todo.done" />
      </label>
      <div class="todo-content">
              <input type="text" v-model="todo.todo" />
            </div>

      <div class="actions">
        <button class="delete" @click="deleteTodo(todo)">Delete</button>
      </div>
    </div>  
     </div> 
    </section>
   </div>
      
    

  </main>
  


</template>
<style>
.title{
  text-align: center;
  font-size:xxx-large;
}
.create-todo{
  text-align: center;
  font-size: x-large;
}
.todo-section{
  text-align: center;
  font-size: x-large;
}
.todo-list{
  font-size: xx-large;
}
.create-todo{
  margin: 0 auto;
}
</style>