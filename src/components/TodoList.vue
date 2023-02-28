<template>
  <div class="todo-list--main-container">
    <h1>Todo List</h1>
    <form
      ref="formRef"
      class="todo-list--form-container"
      @submit="handleSubmit"
    >
      <div class="todo-list--input-container">
        <label for="todo-content">Todo content</label>
        <input id="todo-content" type="text" name="todo-content" required />
      </div>
      <button>Submit</button>
    </form>
    <ul class="todo-list--list-container">
      <li v-for="(item, index) in todoItemsList" :key="item.id">
        <div class="todo-list--list-item">
          <span>
            {{ item.content }}
          </span>
          <button @click="handleDelete(index)">Delete</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script lang="ts" setup>
const TODO_ITEMS_LIST_LS_KEY = 'todoItemsList'

type TodoItem = {
  id: string
  createdAt: string
  content: string
}

const todoItemsList = ref<TodoItem[]>([])
const formRef = ref<HTMLFormElement | null>(null)

function handleSubmit(event: Event) {
  event.preventDefault()

  if (!formRef.value) {
    throw new Error('Form ref is null')
  }

  const formData = new FormData(formRef.value)
  const content = formData.get('todo-content')

  if (!content || typeof content !== 'string') {
    throw new Error('Incorrect form submission')
  }

  const newTodoItem = {
    id: crypto.randomUUID(),
    createdAt: new Date().toISOString(),
    content
  }
  todoItemsList.value.push(newTodoItem)
  localStorage.setItem(
    TODO_ITEMS_LIST_LS_KEY,
    JSON.stringify(todoItemsList.value)
  )
  formRef.value.reset()
}

function handleDelete(index: number) {
  todoItemsList.value.splice(index, 1)
  localStorage.setItem(
    TODO_ITEMS_LIST_LS_KEY,
    JSON.stringify(todoItemsList.value)
  )
}

onMounted(() => {
  const lsTodoItemsList = localStorage.getItem(TODO_ITEMS_LIST_LS_KEY)

  if (!lsTodoItemsList) {
    return
  }

  todoItemsList.value = JSON.parse(lsTodoItemsList)
})
</script>

<style scoped>
.todo-list--main-container {
  max-width: 300px;
}
.todo-list--form-container {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.todo-list--input-container {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.todo-list--list-container {
  display: flex;
  flex-direction: column;
  gap: 16px;
}
.todo-list--list-item {
  display: flex;
  justify-content: space-between;
}
</style>
