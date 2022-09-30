<script setup>
  import {computed, ref} from 'vue'
  
  let id = 0
  const newTodo = ref('')
  const completed = ref(false)
  const todos = ref([
    {id: id++, text: 'Learn html', done: false},
    {id: id++, text: 'Learn css', done: false},
    {id: id++, text: 'Learn javascript', done: false}
  ])

  function addTodo(){
    todos.value.push({id: id++, text: newTodo.value})
    newTodo.value = ''
  }

  function removeTodo(todo){
    todos.value = todos.value.filter((target)=> target !== todo)
  }

  const filteredTodo = computed((t)=>{
    return completed.value ? todos.value.filter((t)=> !t.done): todos.value
  })

</script>

<template>
  <div>
    <form @submit.prevent="addTodo">
      <input type="text" v-model="newTodo">
      <button>Add Todo</button>
    </form>
    <ul>
      <li v-for="todo in filteredTodo" :key="todo.id" :class="{done: todo.done}"><input type="checkbox" v-model="todo.done"/><span class="checkbox"></span>{{todo.text}} <button @click="removeTodo(todo)">X</button></li>
    </ul>
    <div>
      <button class="showHideBtn" @click="completed = !completed">{{completed? 'Show All':'Hide All Completed'}}</button>
    </div>
  </div>
</template>

<style>
  .showHideBtn{
    padding: 0.75rem 1.5rem;
    margin-top: 1rem;
  }
  .done{
    text-decoration: line-through;
  }
  input{
    font-size: 24px;
    padding: 1rem;
  }
  form button{
    margin-left: 1rem;
    font-size: 18px;
    font-weight: bold;
    text-transform: uppercase;
    padding: 1.35rem 2rem;
    background-color: rgb(73 133 243);
    color: #ffffff;
    border: none;
    cursor: pointer;
  }
  ul{
    list-style-type: none;
    margin: 0;
    padding: 0;
    margin-top: 1.5rem;
  }
  li{
    font-size: 21px;
    font-family: sans-serif;
    letter-spacing: 1px;
    text-transform: uppercase;
    margin: 1rem 0;
    position: relative;
    padding-left: 2.5rem;
  }
  li input[type="checkbox"]{
    position: absolute;
    left: 0;
    top: 0;
    width: 25px;
    height: 25px;
    margin: 0;
    opacity: 0;
    cursor: pointer;
    z-index: 1;
  }
  li input[type="checkbox"]:hover ~ .checkbox{
    background-color: rgb(122, 123, 126);
  }
  li input[type="checkbox"]:checked ~ .checkbox{
    background-color: rgb(26, 105, 224);
  }
   li input[type="checkbox"]:checked ~ .checkbox::after{
    opacity: 1;
  }
  li .checkbox{
    position: absolute;
    left: 0;
    top: 0;
    width: 25px;
    height: 25px;
    background-color: rgb(218, 212, 212);
    display: inline-block;
  }
  li .checkbox::after{
    position: absolute;
    left: 0;
    top: 0;
    content: '';
    width: 15px;
    height: 8px;
    border: 5px solid rgb(236, 243, 236);
    border-width: 0 0 4px 4px;
    transform: rotate(-45deg);
    display: inline-block;
    opacity: 0;
    left: 3px;
    top: 3px;
  }
  li button{
    background-color: rgba(204, 41, 41, 0.795);
    color: #ffffff;
    border: none;
    cursor: pointer;
    padding: 0.5rem 0.75rem;
    position: relative;
    top: -0.25rem;
    left: 0.5rem;
  }
  
  button:hover{
    transform: scale(1.03);
    transition: 0.2s ease-out;
  }
</style>