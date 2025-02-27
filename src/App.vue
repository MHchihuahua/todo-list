<script setup>
import { ref, computed, provide, onMounted, onUnmounted } from 'vue';
import TodoList from './components/TodoList.vue';
import TodoForm from './components/TodoForm.vue';

const isMobile = ref(window.innerWidth < 768);
const showMenu = ref(false);
const todos = ref([
  { id: 0, title: 'Item 1', startDate: '', endDate: '', imageUpload: '', imageUrl: '', content: '' },
  { id: 1, title: 'Item 2', startDate: '', endDate: '', imageUpload: '', imageUrl: '', content: '' }
]);
const activeTodoId = ref(0);
let currentId = 2;

const activeTodo = computed(() => todos.value.find(todo => todo.id === activeTodoId.value) || null);

const addTodo = () => {
  const newTodo = {
    id: currentId++,
    title: `Item ${currentId}`,
    startDate: '',
    endDate: '',
    imageUpload: '',
    imageUrl: '',
    content: ''
  };

  todos.value.push(newTodo);
  activeTodoId.value = newTodo.id;
};

const deleteTodo = () => {
  const index = todos.value.findIndex(todo => todo.id === activeTodoId.value);

  if (index !== -1) {
    todos.value.splice(index, 1);
  }

  activeTodoId.value = todos.value.length > 0 ? todos.value[0].id : null;
};

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
provide('todos', todos);
provide('activeTodoId', activeTodoId);
provide('activeTodo', activeTodo);
provide('setActiveTodoId', (id) => activeTodoId.value = id);
provide('addTodo', addTodo);
provide('deleteTodo', deleteTodo);
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
