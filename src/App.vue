<script setup>
import { ref, onMounted, onUnmounted } from 'vue';
import TodoList from './components/TodoList.vue';
import TodoForm from './components/TodoForm.vue';

const isMobile = ref(window.innerWidth < 768);
const showMenu = ref(false);

const handleResize = () => {
  isMobile.value = window.innerWidth < 768;
  if (!isMobile.value) {
    showMenu.value = false;
  }
};

onMounted(() => {
  window.addEventListener('resize', handleResize);
});
onUnmounted(() => {
  window.removeEventListener('resize', handleResize);
});
provide('isMobile', isMobile);
</script>

<template>
  <div class="container">
    <button v-if="isMobile && !showMenu" class="menu-button" @click="showMenu = true">
      <i class="fa-solid fa-bars"></i>
    </button>
    
    <TodoList v-if="!isMobile || showMenu"  @close="showMenu = false" />

    <TodoForm  />
  </div>
</template>

<style scoped>
.container {
  width: 100%;
  display: flex;
  height: 100vh;
}

.menu-button {
  position: absolute;
  font-size: 24px;
  background-color: transparent;
  margin: 10px 25px;
  border: none;
  cursor: pointer;
  z-index: 10;
}

</style>
