<template>
    <div class="memo">
      <ul>
        <li v-for="(item, idx) in data" :key="idx">{{ item }}</li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {
    setup() {
        const data = [
            "메모 1",
            "메모 2",
            "메모 3",
        ]

        return { data };
    }    
  }
  </script>
  
  <style scoped>
  .memo ul {
    list-style: none;
    padding: 0;
    margin: 0;
  }
  </style>
  