<template>
  <div>
    <div
      class="flex tablet:flex-row flex-col justify-between mx-14 tablet:mx-0"
    >
      <input
        placeholder="Type task name"
        autofocus
        class="italic text-[#bfbfbf] font-[Open_Sans] text-[17px] border-none w-[80%] bg-transparent"
        v-model="inputText"
      />
      <button
        class="text-white mt-10 tablet:mt-0 px-12 py-3 relative overflow-hidden border-white-500 bg-black before:absolute before:bottom-0 before:left-0 before:top-0 before:z-0 before:h-full before:w-0 before:bg-amber-100 before:transition-all before:duration-300 hover:text-black hover:before:left-0 hover:before:w-full transform active:scale-75 transition-transform"
        @click="addItem()"
      >
        <span class="relative font-[Open_Sans]">ADD</span>
      </button>
    </div>
    <div class="border-b-[1px] border-black invisible tablet:visible"></div>
    <TodoListContentListItems
      :items="listItems"
      :removeCallback="removeItem"
      :updateCallback="updateItem"
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
const addItem = async () => {
  if (inputText.value) {
    const { data: newItem } = await useFetch(
      "https://to-do-app.titlos.com/todos",
      {
        method: "post",
        body: {
          title: inputText.value,
        },
      }
    );
    // Push the new element to the items' list
    listItems.value.push(toRaw(newItem.value));

    //Clear the current input value
    inputText.value = "";
  }
};

// Update an item from the list
const updateItem = async (itemId) => {
  if (itemId) {
    await useFetch(`https://to-do-app.titlos.com/todos/${itemId}`, {
      method: "put",
      body: {
        completed: true,
      },
    });
    // Update the corresponding element in the items' list
    let index = listItems.value.findIndex((item) => {
      return item.id === itemId;
    });
    listItems.value[index].completed = true;
  }
};

// Remove an item from the list
const removeItem = async (itemId) => {
  if (itemId) {
    await useFetch(`https://to-do-app.titlos.com/todos/${itemId}`, {
      method: "delete",
    });

    // Remove the corresponding element from the items' list
    let index = listItems.value.findIndex((item) => {
      return item.id === itemId;
    });
    if (index > -1) {
      listItems.value.splice(index, 1);
    }
  }
};
</script>
