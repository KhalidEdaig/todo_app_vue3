<template>
  <div class="container grid grid-cols-1 place-content-center mx-auto">
    <div class="text-center text-xl font-semibold">
      Vue 3 Todo App
    </div>
    <form class="py-16" @submit.prevent="addNewTodo">
      <div class="flex items-center border-b border-teal-500">
        <input
          v-model="newTodo"
          name="newTodo"
          class="appearance-none bg-transparent border-none w-full text-gray-700 mr-3 py-1 px-2 leading-tight focus:outline-none"
          type="text"
          placeholder="New Todo"
          aria-label="Full name"
        />
        <button
          class=" flex-shrink-0 bg-teal-500 hover:bg-teal-700 border-teal-500 hover:border-teal-700 text-sm border-4 text-white py-1 px-6  rounded"
          type="submit"
        >
          Add
        </button>
      </div>
      <div class="py-6" v-if="todos.length > 0">
        <button
          @click="doneAll"
          class="mx-2 bg-green-600 hover:bg-green-800 text-white font-bold py-2 px-4 rounded"
        >
          Completed All
        </button>
      </div>
    </form>
    <div class="my-6 py-6">
      <div
        v-for="(todo, index) in todos"
        :key="todo.id"
        class="grid grid-cols-2 place-content-between bg-blue-100 border-t border-b border-blue-500 text-blue-700 px-4 py-3"
        role="alert"
      >
        <div>
          <p :class="{ 'line-through': todo.done }" class="font-bold">
            {{ todo.content }}
          </p>
        </div>
        <div class="grid grid-cols-2">
          <button
            v-if="todo.done"
            @click="toggleDone(todo)"
            class="mx-2 bg-green-500 hover:bg-green-700 text-white font-bold py-2 px-4 rounded"
          >
            Completed
          </button>
          <button
            @click="toggleDone(todo)"
            v-else
            class="mx-2 bg-yellow-500 hover:bg-yellow-700 text-white font-bold py-2 px-4 rounded"
          >
            Not Completed
          </button>
          <button
            @click="removeTodo(todo, index)"
            class=" mx-2 bg-red-500 hover:bg-red-700 text-white font-bold py-2 px-4 rounded"
          >
            Delete
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
export default {
  setup() {
    /*   const data = new reactive({
      newTodo,
      tods: [],
    }); */
    const newTodo = ref("");
    const todos = ref([]);
    function addNewTodo() {
      if (newTodo.value != "") {
        todos.value.push({
          id: Date.now(),
          done: false,
          content: newTodo.value,
        });
        newTodo.value = "";
      }
    }
    function toggleDone(todo) {
      todo.done = !todo.done;
    }
    function removeTodo(todo, index) {
      if (todo.done) {
        todos.value.splice(index, 1);
      }
    }
    function doneAll() {
      todos.value.forEach((todo) => {
        if (!todo.done) {
          todo.done = true;
        }
      });
    }

    return {
      //data,
      doneAll,
      removeTodo,
      toggleDone,
      todos,
      newTodo,
      addNewTodo,
    };
  },
};
</script>

<style></style>
