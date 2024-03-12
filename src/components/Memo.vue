<template>
    <div class="memo container mx-auto w-2/3 py-16">
        <div class="flex justify-end mb-3">
            <button 
                type="button" 
                @click="add"
                class="text-gray-500 bg-white border border-gray-300 focus:outline-none hover:bg-gray-100 focus:ring-4 focus:ring-gray-100 font-medium rounded-full text-sm px-8 py-2.5 me-2 mb-2 dark:bg-gray-800 dark:text-white dark:border-gray-600 dark:hover:bg-gray-700 dark:hover:border-gray-600 dark:focus:ring-gray-700"
                >
                메모 추가
            </button>
        </div>
        <ul class="border-t py-8">
            <li v-for="(item, idx) in data" :key="idx">{{ item }}</li>
        </ul>
    </div>
  </template>
  
  <script>
import { ref } from 'vue';
  export default {
    setup() {
        const data = ref([
            "메모 1",
            "메모 2",
            "메모 3",
        ]);
        
        const add = () => {
            data.value.push("추가 메모");
        }

        return { data, add };
    }    
  }
  </script>
  
  <style scoped>
  .memo ul {
    list-style: none;
  }
  </style>
  