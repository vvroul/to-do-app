<template>
  <div class="flex flex-col w-screen">
    <span class="font-[Open_Sans] text-[20px] cursor-default"> New task </span>
    <div class="border-b-2 border-black mt-2"></div>
    <div class="flex flex-row justify-between">
      <input
        placeholder="Type task name"
        class="italic text-[#bfbfbf] font-[Open_Sans] text-[17px] border-none w-[80%] bg-transparent"
      />
      <button
        class="text-white px-12 py-3 relative overflow-hidden border-white-500 bg-black before:absolute before:bottom-0 before:left-0 before:top-0 before:z-0 before:h-full before:w-0 before:bg-white before:transition-all before:duration-300 hover:text-black hover:before:left-0 hover:before:w-full transform active:scale-75 transition-transform"
      >
        <span class="relative">ADD</span>
      </button>
    </div>
    <div class="border-b-[1px] border-black"></div>
  </div>
</template>
