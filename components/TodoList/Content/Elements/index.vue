<template>
  <div>
    <div
      class="flex tablet:flex-row flex-col justify-between mx-14 tablet:mx-0"
    >
      <input
        placeholder="Type task name"
        class="italic text-[#bfbfbf] font-[Open_Sans] text-[17px] border-none w-[80%] bg-transparent"
        v-model="inputText"
      />
      <button
        class="text-white mt-10 tablet:mt-0 px-12 py-3 relative overflow-hidden border-white-500 bg-black before:absolute before:bottom-0 before:left-0 before:top-0 before:z-0 before:h-full before:w-0 before:bg-white before:transition-all before:duration-300 hover:text-black hover:before:left-0 hover:before:w-full transform active:scale-75 transition-transform"
        @click="addItemToList()"
      >
        <span class="relative font-[Open_Sans]">ADD</span>
      </button>
    </div>
    <div class="border-b-[1px] border-black invisible tablet:visible"></div>
    <TodoListContentListItems
      :items="listItems"
      :removeCallback="removeItemFromList"
      :updateCallback="updateItemFromList"
    />
  </div>
</template>

<script setup>
import { ref } from "vue";

const inputText = ref("");
let listItems = ref([]);

// Get the items from the API
const { data: items } = await useFetch("https://to-do-app.titlos.com/todos");
listItems.value = toRaw(items.value);

// Add a new item to the list, binded to the input's text
const addItemToList = async () => {
  if (inputText.value) {
    await $fetch("https://to-do-app.titlos.com/todos", {
      mode: "no-cors",
      method: "post",
      body: {
        title: inputText.value,
      },
    });
  }
};

// Update an item from the list
const updateItemFromList = async (itemId) => {
  if (itemId) {
    await $fetch(`https://to-do-app.titlos.com/todos/${itemId}`, {
      headers: {
        "Access-Control-Allow-Origin": "*",
      },
      method: "put",
      body: {
        completed: true,
      },
    });
  }
};

// Remove an item from the list
const removeItemFromList = async (itemId) => {
  if (itemId) {
    await $fetch(`https://to-do-app.titlos.com/todos/${itemId}`, {
      headers: {
        "Access-Control-Allow-Origin": "*",
      },
      method: "delete",
    });
  }
};
</script>
