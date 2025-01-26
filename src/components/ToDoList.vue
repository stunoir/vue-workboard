<script setup>
  import { ref, onMounted, watch } from 'vue'

  const props = defineProps({
    view: {
      type: String,
      default() {
        return 'todo'
      }
    }
  })

  const newTask = ref('')
  const newTaskCate = ref('work')
  const tasks = ref([])

  // load tasks from localStorage
  onMounted(() => {
    const storedTasks = localStorage.getItem(`${props.view}-tasks`)
    if (storedTasks) {
      tasks.value = JSON.parse(storedTasks)
    }
  })

  // watch for changes and update localStorage
  watch(
    tasks,
    (newTasks) => {
      localStorage.setItem(`${props.view}-tasks`, JSON.stringify(newTasks))
    },
    { deep: true }
  )

  // add a new task
  const addTask = async () => {
    if (!newTask.value.trim()) return

    tasks.value.push({
      id: Date.now(), // unique ID
      title: newTask.value.trim(),
      category: newTaskCate.value
    })

    newTask.value = ''
  }

  // delete task by ID
  const deleteTask = (id) => {
    tasks.value = tasks.value.filter((task) => task.id !== id)
  }
</script>

<template>
  <div class="component-container">
    <h2 class="text-md">{{ props.view }} List</h2>
    <!-- list form -->
    <form @submit.prevent="addTask" class="form-general m-b-0">
      <label :for="props.view">enter your task</label>

      <div class="grid-x grid-padding-x">
        <div class="cell medium-9 large-10">
          <input
            :id="props.view"
            v-model="newTask"
            autocomplete="off"
            type="text"
            placeholder="enter your task here..."
          />
        </div>
        <div class="cell medium-3 large-2">
          <button type="submit" class="btn-main btn-main--expanded btn-main--xs">add task</button>
        </div>
      </div>
    </form>
    <!-- task list items -->
    <div v-if="tasks.length > 0" class="task-list m-t-1" :class="props.view">
      <div v-for="task in tasks" :key="task.id" class="item">
        <p>{{ task.title }}</p>
        <button @click="deleteTask(task.id)" class="btn-main btn-main--xs">done</button>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped></style>
