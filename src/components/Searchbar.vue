<template>
  <div class="search-box">
    <button class="btn-search" @click="emitSearch">
      <Search class="search-icon"
        color="black"
      />
    </button>
    <input class="input-search" type="text" placeholder="Search for pics..." @keyup.enter="emitSearch" v-model="query" />
  </div>
  
  
</template>

<script setup>
import { ref, defineEmits } from 'vue';
import { Search } from 'lucide-vue-next';

const query = ref("");
const emits = defineEmits(['search']);

const resetSearchField = () => {
  query.value = '';
};



const emitSearch = () => {
  emits('search', query.value);
  resetSearchField();
};
</script>

<style scoped>
.search-box{
  width: fit-content;
  height: fit-content;
  position: relative;
}
.input-search{
  height: 50px;
  width: 50px;
  border-style: none;
  padding: 10px;
  font-size: 18px;
  letter-spacing: 2px;
  outline: none;
  border-radius: 25px;
  transition: all .5s ease-in-out;
  background-color: #2195f360;
  padding-right: 40px;
  color:#fff;
}
.input-search::placeholder{
  color:rgba(255,255,255,.5);
  font-size: 18px;
  letter-spacing: 2px;
  font-weight: 100;
}
.btn-search{
  width: 50px;
  height: 50px;
  border-style: none;
  font-size: 20px;
  font-weight: bold;
  outline: none;
  cursor: pointer;
  border-radius: 50%;
  position: absolute;
  right: 0px;
  color:#ffffff ;
  background-color:transparent;
  pointer-events: painted;  
}
.btn-search:focus ~ .input-search{
  width: 300px;
  border-radius: 0px;
  background-color: transparent;
  border-bottom:1px solid rgba(255,255,255,.5);
  transition: all 500ms cubic-bezier(0, 0.110, 0.35, 2);
}
.input-search:focus{
  width: 300px;
  border-radius: 0px;
  background-color: transparent;
  border-bottom:1px solid rgba(255,255,255,.5);
  transition: all 500ms cubic-bezier(0, 0.110, 0.35, 2);
}

.search-icon {
  transform: translateY(3px);
}
</style>
