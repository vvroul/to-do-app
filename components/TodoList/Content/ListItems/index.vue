<template>
  <div class="mt-20">
    <div
      v-for="item in items"
      class="hover:transition ease-in-out delay-20 hover:-translate-y-1 hover:bg-amber-100 hover:scale-200 duration-500 cursor-pointer"
    >
      <div
        class="flex flex-row justify-between items-center max-w cursor-pointer"
      >
        <span
          class="font-[Open_Sans] text-[17px]"
          :class="{ 'line-through': item.completed }"
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
            class="cursor-pointer mt-4"
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
