<template>
  <main>
    <header>
      <img src="./assets/pinia-logo.svg" alt="pinia-logo"/>
      <h1>Pinia Tasks</h1>
    </header>

    <nav class="filter">
      <button @click="filter = 'all'">All Tasks</button>
      <button @click="filter = 'favs'">Fav Tasks</button>
    </nav>

    <div class="task-list" v-if="filter === 'all'">
      <div v-for="task in taskStore.tasks">
        <TaskDetails :task="task" />
      </div>
    </div>

    <div class="task-list"  v-if="filter === 'favs'">
      <div v-for="task in taskStore.favs">
        <TaskDetails :task="task" />
      </div>
    </div>
  </main>

</template>

<script>
  import { useTaskStore } from './stores/TaskStore'
  import TaskDetails from '@/components/TaskDetails.vue'
  import { ref } from 'vue'

  export default {
    setup () {
      const taskStore = useTaskStore()

      const filter = ref('all')

      return { taskStore, filter }
    },
    components: {
      TaskDetails
    }
  }
</script>