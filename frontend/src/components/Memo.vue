<template>
    <div class="memo container mx-auto w-2/3 py-16">
        <div class="flex justify-center mb-3">
            <input 
                type="text" 
                v-model="inputValue"
                class="mr-4 bg-gray-50 border border-gray-300 text-gray-900 text-base rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-4/5 py-2.5 px-5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" 
                placeholder="메모할 내용을 입력해보세요." 
                required 
                />
            <button 
                type="button" 
                @click="add"
                class="text-gray-500 bg-white border border-gray-300 focus:outline-none hover:bg-gray-100 focus:ring-4 focus:ring-gray-100 font-medium rounded-full text-sm px-8 py-2.5 me-2 dark:bg-gray-800 dark:text-white dark:border-gray-600 dark:hover:bg-gray-700 dark:hover:border-gray-600 dark:focus:ring-gray-700"
                >
                메모 추가
            </button>
        </div>
        <ul class="border-t py-8 px-7">
            <li v-for="(item, idx) in data" :key="idx">
                <span @click="onDelete(idx)" class="mr-2 cursor-pointer">🟨</span>
                {{ item }}</li>
        </ul>
    </div>
  </template>
  
  <script>
    import axios from 'axios';
    import { ref } from 'vue';

  export default {
    setup() {
        const data = ref([]);
        const inputValue = ref("");

        // 데이터 패치
        axios.get("/api/memo")
            .then((res) => {
                data.value = res.data;
            })
            .catch(err => console.log(err))

        // 데이터 추가
        const add = () => {
            if(inputValue.value.trim()) {
                axios.post("/api/memo", { content: inputValue.value })
                    .then((res) => {
                        data.value = res.data;
                        inputValue.value = "";
                    })
            } else {
                alert("메모를 입력하세요.");
            }
        }

        // 데이터 삭제
        const onDelete = (idx) => {
            axios.delete(`/api/memo/${idx}`) 
                .then((res) => {
                        data.value = res.data;
                    })          
        }
       

        return { data, add, inputValue, onDelete };
    }    
  }
  </script>
  
  <style scoped>
  .memo ul {
    list-style: none;
  }

  .memo ul li {
    margin-bottom: 24px;
    font-size: larger;
    font-weight: 300;
  }
  </style>
  