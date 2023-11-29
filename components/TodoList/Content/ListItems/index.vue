<template>
  <div class="mt-20">
    <div v-for="item in items">
      <div class="flex flex-row justify-between items-center max-w">
        <span class="font-[Open_Sans] text-[17px]"> {{ item.title }} </span>
        <img
          alt="deleteIcon"
          src="@/assets/img/delete_icon.svg"
          width="20"
          height="20"
          class="cursor-pointer mt-4"
        />
      </div>
      <div class="border-b-[1px] mt-4 border-gray-400"></div>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  items: Array,
});
</script>
