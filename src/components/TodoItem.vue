<template>
  <div
    class="grid grid-cols-[1fr_auto_auto_auto] gap-2 mb-4 items-center border rounded-lg p-2"
  >
    <input
      v-model="newItem"
      type="text"
      class="text-black pb-2 pl-4 outline-none"
    />

    <button
      @click="deleteItem"
      type="button"
      class="text-blue-500 px-2 py-2 flex items-center"
    >
      <TrashIcon class="w-4 h-4 mr-1" />
      حذف
    </button>

    <button
      @click="editeItem"
      type="button"
      class="text-red-600 flex items-center"
    >
      <PencilIcon class="w-4 h-4 mr-1" /> ویرایش
    </button>
    <div class="flex items-center justify-center mr-2">
      <input v-model="completet" type="checkbox" class="ml-2" />
      <CheckIcon class="w-4 h-4 ml-1" />
    </div>
  </div>
</template>
<script setup>
import { PencilIcon, TrashIcon, CheckIcon } from "@heroicons/vue/24/solid";
import { ref } from "vue";
const props = defineProps({ todo: Object });
const newItem = ref(props.todo.text);

const emit = defineEmits(["deleteItem", "editeItem"]);

const deleteItem = () => {
  emit("deleteItem", props.todo.id);
};
</script>
