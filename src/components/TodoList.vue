<template>
    <h1>To-do list</h1>
    <div class="container">
        <button @click="createItem" :style="{ width: '500px' }">Add new to-do</button>
        <div v-for=" item in listItems" class="todo-items" :key="item.id">
            <div class="msg-block">
                <input v-if="item.isEditing" v-model="item.msg" />
                <div v-else>{{ item.msg }}</div>
                <!-- 通过v-model实现双向绑定 -->
            </div>
            <div class="btn-block">
                <button @click="toggleEditing(item)">{{ item.isEditing ? 'Save' : 'Edit' }}</button>
                <button @click="deleteItem(item)">Delete</button>
            </div>
        </div>
    </div>

</template>
<script lang="ts" setup>
import { ref } from 'vue';

type Item = { id: string, msg: string, isEditing?: boolean }
const listItems = ref<Item[]>([{ id: '1', msg: 'First to-do' }])

const createItem = () => {
    const newItem = { id: 'id' + Date.now(), msg: "New to-do" }
    listItems.value.push(newItem)
}
const deleteItem = ({ id }: { id: string }) => {
    listItems.value = listItems.value.filter(e => e.id !== id)
}
const toggleEditing = (item: Item) => {
    // 每个listItem都有自己的editing状态，虽然item列表是在ref中定义，但可以直接在item上单独修改它的editing状态
    item.isEditing = !item.isEditing
}
</script>
<style>
.todo-items {
    width: 500px;
    margin: 5px auto;
    display: flex;
    justify-content: space-between;
    align-items: center;
    height: 30px;

}

input {
    font-size: 16px;
}

.msg-block {}

.btn-block {
    button {
        width: 100px;
        margin-left: 10px;
        /* height: 30px; */
    }
}
</style>