<template>
  <div class="mt-20">
    <div
      v-for="item in items"
      class="hover:transition ease-in-out delay-20 hover:-translate-y-1 hover:bg-amber-100 hover:scale-200 duration-500 cursor-pointer"
    >
      <div
        class="flex flex-row tablet:justify-between justify-evenly items-center w-[100%] cursor-pointer"
      >
        <span
          class="font-[Open_Sans] text-[17px] w-[200px] tablet:w-full break-words"
          :class="{ 'line-through font-bold italic': item.completed }"
          @click="updateCallback(item.id)"
        >
          {{ item.title }}
        </span>
        <button @click="removeCallback(item.id)">
          <img
            alt="deleteIcon"
            src="@/assets/img/delete_icon.svg"
            width="20"
            height="20"
            class="cursor-pointer mt-4 hover:-translate-y-2 hover:scale-600 duration-100"
          />
        </button>
      </div>
      <div class="border-b-[1px] mt-4 border-gray-400"></div>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  items: Array,
  removeCallback: Function,
  updateCallback: Function,
});
</script>
