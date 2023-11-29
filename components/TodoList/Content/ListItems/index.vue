<template>
  <div class="mt-20">
    <div v-for="item in items">
      <div
        class="flex flex-row justify-between items-center max-w cursor-pointer"
      >
        <span
          @click="updateTask(item)"
          class="font-[Open_Sans] text-[17px]"
          :class="{ 'line-through': item.completed }"
        >
          {{ item.title }}
        </span>
        <button>
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

const updateTask = (item) => {
  item.completed = true;
};
</script>
