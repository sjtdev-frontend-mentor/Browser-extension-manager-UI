<template>
  <header class="my-10 flex h-16 w-full items-center justify-between rounded-2xl border-stone-400 bg-slate-50 p-3 shadow-[0_0_8px] shadow-stone-400/40 dark:bg-[#1F2535]">
    <img :src="`images/logo-${darkMode ? 'dark' : 'light'}.svg`" alt="" />
    <button
      class="flex h-10 w-10 items-center justify-center rounded-xl bg-neutral-200 transition-colors duration-150 hover:bg-stone-400 focus:outline-2 focus:outline-offset-2 focus:outline-red-700 dark:bg-[#2F354C] dark:hover:bg-[#525868] dark:focus:bg-[#56586A] dark:focus:outline-[#D76667]"
      @click="toggleDarkMode()"
    >
      <img class="h-5 w-5" :src="`images/icon-${darkMode ? 'sun' : 'moon'}.svg`" alt="" />
    </button>
  </header>
  <div class="my-6 flex flex-col items-center justify-between gap-6 md:flex-row">
    <p class="text-3xl font-extrabold dark:text-white">Extensions List</p>
    <div class="flex items-center gap-4 md:gap-2">
      <button
        class="h-12 rounded-3xl border-stone-400 px-5 text-base font-medium shadow-[0_0_8px] shadow-stone-400/40 transition-colors duration-150 hover:opacity-70 focus:outline-2 focus:outline-offset-2 focus:outline-red-700 md:h-10 md:px-4 md:text-sm dark:hover:opacity-100 dark:focus:outline-[#D76667]"
        :class="{ 'bg-red-700 text-slate-50 dark:bg-[#F25C55] dark:text-[#04091C] dark:hover:!opacity-70': option.value === filter, 'bg-slate-50 dark:bg-[#2F354B] dark:text-slate-50 dark:hover:brightness-125': option.value !== filter }"
        v-for="option in filterOptions"
        :key="option.value"
        @click="filter = option.value"
      >
        {{ option.label }}
      </button>
    </div>
  </div>
  <div class="grid grid-cols-[repeat(auto-fill,minmax(343px,1fr))] justify-items-center gap-3 md:grid-cols-[repeat(auto-fill,minmax(382px,1fr))] mb-10">
    <Card @remove="removeCard" v-for="(card, index) in cards" :key="index" v-model="cards[index]" v-show="shouldShowItem(card)" class="w-full max-w-[343px] md:max-w-[382px]" />
  </div>
</template>

<script setup>
import Card from "./components/Card.vue";
import { ref, onMounted, computed } from "vue";

const darkMode = ref(false);
const filter = ref("all");
const filterOptions = [
  { value: "all", label: "All" },
  { value: "active", label: "Active" },
  { value: "inactive", label: "Inactive" },
];

const cards = ref([]);

onMounted(() => {
  cards.value = [
    {
      title: "DevLens",
      description: "Quickly inspect page layouts and visualize element boundaries.",
      image: "images/logo-devlens.svg",
      active: true,
    },
    {
      title: "StyleSpy",
      description: "Instantly analyze and copy CSS from any webpage element.",
      image: "images/logo-style-spy.svg",
      active: true,
    },
    {
      title: "SpeedBoost",
      description: "Optimizes browser resource usage to accelerate page loading.",
      image: "images/logo-speed-boost.svg",
      active: false,
    },
    {
      title: "JSONWizard",
      description: "Formats, validates, and prettifies JSON responses in-browser.",
      image: "images/logo-json-wizard.svg",
      active: true,
    },
    {
      title: "TabMaster Pro",
      description: "Organizes browser tabs into groups and sessions.",
      image: "images/logo-tab-master-pro.svg",
      active: true,
    },
    {
      title: "ViewportBuddy",
      description: "Simulates various screen resolutions directly within the browser.",
      image: "images/logo-markup-notes.svg",
      active: false,
    },
    {
      title: "Markup Notes",
      description: "Enables annotation and notes directly onto webpages for collaborative debugging.",
      image: "images/logo-markup-notes.svg",
      active: true,
    },
    {
      title: "GridGuides",
      description: "Overlay customizable grids and alignment guides on any webpage.",
      image: "images/logo-grid-guides.svg",
      active: false,
    },
    {
      title: "Palette Picker",
      description: "Instantly extracts color palettes from any webpage.",
      image: "images/logo-palette-picker.svg",
      active: true,
    },
    {
      title: "LinkChecker",
      description: "Scans and highlights broken links on any page.",
      image: "images/logo-link-checker.svg",
      active: true,
    },
    {
      title: "DOM Snapshot",
      description: "Capture and export DOM structures quickly.",
      image: "images/logo-dom-snapshot.svg",
      active: false,
    },
    {
      title: "ConsolePlus",
      description: "Enhanced developer console with advanced filtering and logging.",
      image: "images/logo-console-plus.svg",
      active: true,
    },
  ];
});

const toggleDarkMode = () => {
  if (darkMode.value) document.documentElement.classList.remove("dark");
  else document.documentElement.classList.add("dark");
  darkMode.value = !darkMode.value;
};

const shouldShowItem = computed(() => (item) => {
  if (filter.value === "all") return true;
  return filter.value === "active" ? item.active : !item.active;
});

function removeCard(item){
  cards.value = cards.value.filter((card) => card !== item);
}
</script>
