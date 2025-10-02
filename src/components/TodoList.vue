<template>
  <div class="max-w-md mx-auto p-4 bg-white shadow-lg rounded-lg">
    <h1 class="text-2xl font-bold mb-4 text-center text-gray-800">
      لیست وظایف
    </h1>
    <div class="grid grid-cols-[1fr_auto] gap-2 mb-4">
      <input
        v-model="newTodo"
        @keyup.enter="addTodo"
        type="text"
        placeholder="وظیفه جدید را وارد کنید"
        class="p-2 border rounded-lg focus:outline-none focus:right-2 focus:ring-blue-500"
      />
      <button
        @click="addTodo"
        type="submit"
        class="flex items-center bg-blue-500 text-white px-4 py-2 rounded-lg hover:bg-blue-600 transition"
      >
        <PlusIcon class="w-4 h-4 mr-1" />
        افزودن
      </button>
    </div>

    <div class="space-y-2">
      <TodoItem
        v-for="todo in todos"
        :key="todo.id"
        :todo="todo"
        @deleteItem="handleDelete"
        @editeItem="handleEdite"
      />
    </div>
  </div>
</template>

<script setup>
import { PlusIcon } from "@heroicons/vue/24/solid";

import { onMounted, ref, watch } from "vue";
import TodoItem from "./TodoItem.vue";

const todos = ref([]);
onMounted(() => {
  const saved = localStorage.getItem("todos");
  if (saved) {
    todos.value = JSON.parse(saved);
  }
});

watch(
  todos,
  (newValue) => {
    localStorage.setItem("todos", JSON.stringify(newValue));
  },
  { deep: true }
);

const newTodo = ref("");
const addTodo = () => {
  if (newTodo.value.trim()) {
    todos.value.push({
      id: Date.now(),
      text: newTodo.value,
      completed: false,
    });
    newTodo.value = "";
  }
};

const handleDelete = (id) => {
  todos.value = todos.value.filter((todo) => todo.id !== id);
};

const handleEdite = ({ id, text }) => {
  todos.value = todos.value.map((todo) => {
    if (todo.id === id) {
      return { ...todo, text: text };
    }
    return todo;
  });
};
</script>
