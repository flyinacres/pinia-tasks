<template>
  <main>
    <header>
      <img src="./assets/pinia-logo.svg" alt="pinia-logo"/>
      <h1>Pinia Tasks</h1>
    </header>

    <div class="new-task-form">
      <TaskForm />
    </div>

    <nav class="filter">
      <button @click="filter = 'all'">All Tasks</button>
      <button @click="filter = 'favs'">Fav Tasks</button>
    </nav>

    <!-- loading -->
    <div class="loading" v-if="loading">Loading tasks...</div>

    <div class="task-list" v-if="filter === 'all'">
      <p>You have {{ totalCount }} task(s) to do</p>
      <div v-for="task in tasks">
        <TaskDetails :task="task" />
      </div>
    </div>

    <div class="task-list"  v-if="filter === 'favs'">
      <p>You have {{ favCount }} favorite task(s) to do</p>
      <div v-for="task in favs">
        <TaskDetails :task="task" />
      </div>
    </div>

    <button @click="taskStore.$reset">reset state</button>
  </main>

</template>

<script>
  import { useTaskStore } from './stores/TaskStore'
  import TaskDetails from '@/components/TaskDetails.vue'
  import TaskForm from '@/components/TaskForm.vue'
  import { ref } from 'vue'
  import { storeToRefs } from 'pinia'

  export default {
    setup () {
      const taskStore = useTaskStore()

      // Could grab all of the data off of the store, and use them without prepending 'taskStore'
      // but you cannot get actions this way.
      const {tasks, loading, favs, totalCount, favCount} = storeToRefs(taskStore)

      taskStore.getTasks()

      const filter = ref('all')

      return { taskStore, filter, tasks, loading, favs, totalCount, favCount }
    },
    components: {
      TaskDetails, TaskForm
    }
  }
</script>