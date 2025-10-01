<template>
  <div class="flex flex-row border rounded-lg mb-4">
    <input v-model="newItem" type="text" class="text-black pb-2" />

    <button @click="deleteItem" type="button" class="text-blue-500 px-2">
      حذف
    </button>
    <button @click="editeItem" type="button" class="text-red-600">
      ویرایش
    </button>
  </div>
</template>
<script setup>
import { ref } from "vue";
const props = defineProps({ todo: Object });
const newItem = ref(props.todo.text);

const emit = defineEmits(["deleteItem", "editeItem"]);

const deleteItem = () => {
  emit("deleteItem", props.todo.id);
};

const editeItem = () => {
  emit("editeItem", { id: props.todo.id, text: newItem.value });
};
</script>
