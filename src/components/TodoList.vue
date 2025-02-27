<script setup>
import { ref, defineEmits, inject, computed, onMounted } from 'vue';

const emit = defineEmits(['close']);

const isMobile = inject('isMobile');
const todos = inject('todos');
const activeTodoId = inject('activeTodoId');
const setActiveTodoId = inject('setActiveTodoId');
const addTodo = inject('addTodo');
</script>

<template>
    <div v-if="isMobile" class="todo-list-mask"></div>
    <div class="todo-list-wrapper">
        <div class="todo-list">
            <button v-if="isMobile" class="close-btn" @click="emit('close')">
                <i class="fa-solid fa-xmark"></i>
            </button>
            <p class="todo-list-title">Demo Todo List</p>
            <ol class="todo-list-items">
                <li v-for="(todo, index) in todos" :key="todo.id"
                    :class="['todo-item', { 'todo-item--active': todo.id === activeTodoId }]"
                    @click="setActiveTodoId(todo.id)">
                    {{index + 1}}. {{todo.title}}
                </li>
            </ol>
            <button class="add-btn" @click="addTodo" :disabled="disabledAddButton">Add Item</button>
        </div>
        <div class="image-container">
            <div class="image"></div>
        </div>
    </div>
</template>

<style scoped>
.todo-list-wrapper {
    width: 250px;
    background: #A1FFC7;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    justify-items: center;
}

.todo-list-title {
    font-size: 20px;
    font-weight: 500;
    padding: 15px 20px;
}

.close-btn {
    position: absolute;
    top: 15px;
    right: 15px;
    border: none;
    background: none;
    cursor: pointer;
}

.add-btn {
    width: 210px;
    height: 45px;
    margin: 20px;
    padding: 9px 39px;
}

.todo-list-items {
    cursor: pointer;
    padding: 0;
}

.todo-item {
    display: flex;
    align-items: center;
    margin: 5px 0;
    padding: 4px 14px;
    height: 48px;
    background-color: #81F8B1;
}

.todo-item--active {
    font-weight: 700;
    position: relative;
}

.todo-item--active::after {
    content: "";
    position: absolute;
    top: 50%;
    right: 0;
    transform: translateY(-50%);
    width: 55px;
    height: 100%;
    background-color: #fff;
    clip-path: polygon(100% 0%, 50% 50%, 100% 100%);
}

.image-container {
    display: flex;
    justify-content: center;
    padding: 20px;
}

.image {
    width: 210px;
    height: 60px;
    background-color: #ebebeb;
    border-radius: 10px;
}



@media (max-width: 768px) {
    .todo-list-wrapper {
        position: absolute;
        left: 0;
        top: 0;
        height: 100vh;
        z-index: 2;
    }

    .todo-list-mask {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: rgba(0, 0, 0, 0.5);
        z-index: 1;
    }

}
</style>
