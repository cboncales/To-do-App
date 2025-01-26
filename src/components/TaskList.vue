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
            <!-- Title and Add Task Button -->
            <div class="d-flex justify-space-between">
              <v-card-title class="my-2">Today's Tasks</v-card-title>
              <v-btn
                class="mx-5 my-3"
                density="compact"
                size="large"
                icon="mdi-plus"
                color="blue-darken-1"
                @click="isVisible = true"
              ></v-btn>
            </div>
            <v-card-text>
              <!-- Task List -->
              <v-row dense>
                <v-col
                  v-for="task in tasks"
                  :key="task.id"
                  cols="12"
                  sm="6"
                  md="4"
                  lg="3"
                  :class="{ 'blue-grey lighten-3': task.done }"
                >
                  <v-card class="pa-3" outlined :elevation="task.done ? 1 : 3">
                    <div class="d-flex align-center mb-2">
                      <v-icon
                        @click="doneTask(task.id)"
                        :color="task.done ? 'green' : 'grey'"
                        class="mr-2 cursor-pointer"
                      >
                        {{ task.done ? 'mdi-checkbox-marked' : 'mdi-checkbox-blank-outline' }}
                      </v-icon>
                      <v-text-field
                        v-if="task.editing"
                        v-model="task.title"
                        hide-details
                      ></v-text-field>
                      <span
                        v-else
                        @dblclick="task.editing = true"
                        :class="{
                          'text-decoration-line-through': task.done,
                          'text-success': task.done,
                        }"
                        class="font-weight-medium"
                      >
                        {{ task.title }}
                      </span>
                      <v-spacer></v-spacer>
                      <span
                        class="text-caption"
                        :class="{
                          'text-decoration-line-through': task.done,
                          'text-success': task.done,
                        }"
                      >
                        {{ task.time }}
                      </span>
                    </div>
                    <v-divider class="my-2"></v-divider>
                    <div class="d-flex justify-space-between">
                      <v-btn icon small @click.stop="editTask(task)">
                        <v-icon color="green" size="small">
                          {{ task.editing ? 'mdi-check' : 'mdi-pencil' }}
                        </v-icon>
                      </v-btn>
                      <v-btn icon small @click.stop="deleteTask(task.id)">
                        <v-icon color="red" size="small">mdi-delete</v-icon>
                      </v-btn>
                    </div>
                  </v-card>
                </v-col>
              </v-row>
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
