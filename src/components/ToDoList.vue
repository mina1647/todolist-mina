<script setup lang="ts">
import { ref } from 'vue'

interface Item {
  task: string
  due: string
}

const items = ref<Item[]>([

])

const doneitems = ref<Item[]>([
  
])

const newTaskName = ref('')
const newTaskDue = ref('')
// const doneTaskName = ref('')
// const doneTaskDue = ref('')

const addItem = () => {
    if (newTaskName.value === '' || newTaskDue.value === '') return
    items.value.push({ task: newTaskName.value, due: newTaskDue.value})
    newTaskName.value = ''
    newTaskDue.value = ''
}


const doneItem = (item: Item) => {

    items.value = items.value.filter(i => i !== item)
    doneitems.value.push({ task: item.task, due: item.due })
    
}



// const count = ref<number>(0)
// const countMessage = computed(() => '回数: ' + count.value)
</script>

<template>
  <div>
    <div>ToDoList</div>
    <div>未完のタスク</div>
    <ul>
      <li v-for="item in items" :key="item.task" >
        <div>やること: {{ item.task }} 期限: {{ item.due }} <button @click="doneItem(item)">完了</button></div>
      </li>
    </ul>
    <div>完了したタスク</div>
    <ul>
      <li v-for="item in doneitems" :key="item.task" >
        <div>やること: {{ item.task }} 期限: {{ item.due }}</div>
      </li>
    </ul>
  </div>
  <div>
        <label>
            やること
            <input v-model="newTaskName" type="text" />
        </label>
        <label>
            期限
            <input v-model="newTaskDue" type="text" />
        </label>
        <button @click="addItem">追加</button>
    </div>
</template>

<style></style>