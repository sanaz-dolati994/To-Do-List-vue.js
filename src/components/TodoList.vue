<template>
  <div class="max-w-md mx-auto p-4 bg-white shadow-lg rounded-lg">
    <h1 class="text-2xl font-bold mb-4 text-center text-gray-800">
      لیست وضایف
    </h1>

    <!-- فرم افزودن یادآوری-->
    <div class="flex gap-2 mb-4">
      <input
        v-model="newTodo"
        @keyup.enter="addTodo"
        type="text"
        placeholder="یادآوری جدید را وارد کنید"
        class="flex-1 p-2 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
      />
      <button
        @click="addTodo"
        class="bg-blue-500 text-white px-4 py-2 rounded-lg hover:bg-blue-600 transition"
      >
        افزودن
      </button>
    </div>

    <!-- لیست یادآوری ها-->
    <div>
      <TodoItem
        v-for="todo in todos"
        :key="todo.id"
        :todo="todo"
        @update="updateTodo"
        @delete="deleteTodo"
      />
    </div>
  </div>
</template>
