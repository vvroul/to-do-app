<template>
  <div>
    <div class="flex flex-row justify-between">
      <input
        placeholder="Type task name"
        class="italic text-[#bfbfbf] font-[Open_Sans] text-[17px] border-none w-[80%] bg-transparent"
        v-model="inputText"
      />
      <button
        class="text-white px-12 py-3 relative overflow-hidden border-white-500 bg-black before:absolute before:bottom-0 before:left-0 before:top-0 before:z-0 before:h-full before:w-0 before:bg-white before:transition-all before:duration-300 hover:text-black hover:before:left-0 hover:before:w-full transform active:scale-75 transition-transform"
        @click="addItemToList()"
      >
        <span class="relative font-[Open_Sans]">ADD</span>
      </button>
    </div>
    <div class="border-b-[1px] border-black"></div>
    <TodoListContentListItems :items="items" />
  </div>
</template>

<script setup>
import { ref } from "vue";

// Getting the items from the API
const { data: items } = await useFetch("https://to-do-app.titlos.com/todos");

const inputText = ref("");

// Adding items to the list
const addItemToList = async () => {
  await useFetch("https://to-do-app.titlos.com/todos", {
    method: "post",
    body: {
      title: inputText,
    },
    mode: "no-cors",
  });
};
</script>
