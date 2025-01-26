<script setup>
import { ref } from 'vue'
import TaskModal from './layout/TaskModal.vue'

// Reactive tasks list
const tasks = ref([])
const isVisible = ref(false)

// Mark task as done/undone
const doneTask = (id) => {
  const task = tasks.value.find((task) => task.id === id)
  if (task) task.done = !task.done
}

// Delete task
const deleteTask = (id) => {
  tasks.value = tasks.value.filter((task) => task.id !== id)
}

// Edit task
const editTask = (task) => {
  task.editing = !task.editing
}

// Add a new task from TaskModal
const addTask = (newTask) => {
  tasks.value.push(newTask)
}
</script>

<template>
  <v-main style="height: 250px" app>
    <v-container>
      <v-row>
        <v-col cols="12">
          <v-card>
            <div class="d-flex justify-space-between">
              <v-card-title class="my-2">Today's Tasks</v-card-title>
              <v-btn
                class="mx-5 my-1"
                density="compact"
                size="large"
                icon="mdi-plus"
                color="orange-darken-2"
                @click="isVisible = true"
              ></v-btn>
            </div>
            <v-card-text>
              <v-list>
                <v-list-item v-for="task in tasks" :key="task.id">
                  <v-icon @click="doneTask(task.id)">
                    {{ task.done ? 'mdi-checkbox-marked' : 'mdi-checkbox-blank-outline' }}
                  </v-icon>
                  <v-list-item-title>{{ task.title }}</v-list-item-title>
                  <v-list-item-subtitle>{{ task.time }}</v-list-item-subtitle>
                  <v-list-item-action>
                    <v-btn @click.stop="deleteTask(task.id)" icon>
                      <v-icon color="blue-grey darken-1">mdi-delete</v-icon>
                    </v-btn>
                    <v-btn @click.stop="editTask(task)" icon>
                      <v-icon color="blue-grey darken-1">
                        {{ task.editing ? 'mdi-check' : 'mdi-pencil' }}
                      </v-icon>
                    </v-btn>
                  </v-list-item-action>
                </v-list-item>
              </v-list>
            </v-card-text>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
    <!-- TaskModal -->
    <TaskModal
      :isAddTaskVisible="isVisible"
      @update:isAddTaskVisible="isVisible = $event"
      @add-task="addTask"
    ></TaskModal>
  </v-main>
</template>
