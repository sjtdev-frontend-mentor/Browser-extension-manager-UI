<template>
  <div class="flex h-[200px] md:w-[382px] w-[343px] flex-col justify-between rounded-2xl border-[#DAE1EB] dark:border-[#52576A] border bg-slate-50 p-4.5 shadow-[0_0_8px] shadow-stone-400/20 dark:bg-[#1F2535] dark:shadow-[0_0_2px] dark:shadow-[#31384D]">
    <div class="flex gap-4.5">
      <img class="h-15 w-15" :src="card.image" alt="" />
      <div class="flex flex-col gap-1">
        <p class="text-xl font-extrabold dark:text-white">{{ card.title }}</p>
        <p class="dark:text-gray-400">{{ card.description }}</p>
      </div>
    </div>
    <div class="flex items-center justify-between">
      <button
        class="h-[38px] w-[91px] rounded-3xl border border-stone-300 font-semibold transition-colors duration-150 hover:bg-red-700 hover:text-white focus:border-none focus:bg-neutral-300 focus:outline-2 focus:outline-offset-2 focus:outline-red-700 dark:border-[#494F5F] dark:font-medium dark:text-[#ECF3FD] dark:hover:bg-[#F55A56] dark:hover:text-[#04091C] dark:focus:bg-[#52576A] dark:focus:outline-[#D76667]"
        @click="removeCard(card)"
      >
        Remove
      </button>
      <div class="relative inline-block">
        <input :id="'switch-' + card.title" type="checkbox" class="peer sr-only" v-model="card.active" />
        <label
          :for="'switch-' + card.title"
          class="relative block h-5 w-9 cursor-pointer rounded-full bg-gray-300 transition-colors duration-150 peer-checked:bg-red-700 peer-focus:outline-2 peer-focus:outline-offset-2 peer-focus:outline-red-700 hover:opacity-70 dark:bg-[#525868] dark:peer-checked:bg-[#F15C56] dark:peer-focus:outline-[#D76667]"
        >
          <span
            class="absolute top-0.5 h-4 w-4 rounded-full bg-white transition-all"
            :class="{
              'left-0.5': !card.active,
              'left-[calc(100%-1.125rem)]': card.active,
            }"
          ></span>
        </label>
      </div>
    </div>
  </div>
</template>

<script setup>
const card = defineModel();
const emit = defineEmits(["remove"]);

function removeCard(card) {
  emit("remove", card);
}
</script>
