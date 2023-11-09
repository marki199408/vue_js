<template>
  <main style="min-height: 50vh; margin-top: 2rem">
    <div class="container">
      <div class="row">
        <div class="col-md-8 offset-md-2">
          <!-- Add new Task -->

        <NewTask />

          <!-- List of tasks -->
          <Tasks :tasks="uncompletedTasks" 
                  @updated="handleUpdatedTask"
                  @completed="handleCompletedTask"
                  @removed="handleRemovedTask"
          />

          <div class="text-center my-3" v-show="showToggleCompletedBtn">
            <button class="btn btn-sm btn-secondary" @click="showCompletedTask = !showCompletedTask">
              <span v-if="!showCompletedTask">Show completed</span>
              <span v-else>Hide completed</span>
            </button>
          </div>

          <Tasks :tasks="completedTasks" 
                 :show="completedTasksIsVisible && showCompletedTask"
                 @updated="handleUpdatedTask"
                 @completed="handleCompletedTask"
                 @removed="handleRemovedTask"
          />
          
        </div>
      </div>
    </div>
  </main>
</template>

<script setup>
import { computed, onMounted, ref } from 'vue';
import { storeToRefs } from "pinia";
import { useTaskStore } from "../stores/task";
import Tasks from '../components/tasks/Tasks.vue';
import NewTask from '../components/tasks/NewTask.vue';

const store = useTaskStore()
const { completedTasks, uncompletedTasks } = storeToRefs(store)
const { fetchAllTasks} = store

const tasks = ref([])

onMounted(async () => {
    // const {data} = await allTask()

    // tasks.value = data.data
    await fetchAllTasks()

    // console.log(completedTasks.value)
    // console.log(uncompletedTasks.value)
})

// const uncompletedTasks = computed(() => tasks.value.filter(task => !task.is_completed))
// const completedTasks = computed(() => tasks.value.filter(task => task.is_completed))
const showToggleCompletedBtn = computed(() => uncompletedTasks.value.length > 0 && completedTasks.value.length > 0 )
const completedTasksIsVisible = computed(()=> uncompletedTasks.value.length === 0 || completedTasks.value.length > 0)
const showCompletedTask = ref(false)


</script>