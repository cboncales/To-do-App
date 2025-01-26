<script setup>
import { ref, computed, watch } from 'vue'

// Props and emits
const props = defineProps({
  isAddTaskVisible: Boolean, // Accept `isAddTaskVisible` as a prop
})
const emits = defineEmits(['update:isAddTaskVisible', 'add-task']) // Define emits

// Reactive state
const errorMessages = ref('')
const name = ref('')
const time = ref('')
const formHasErrors = ref(false)

// Computed property for form data
const form = computed(() => ({
  name: name.value,
  time: time.value,
}))

// Watcher for name field
watch(name, () => {
  errorMessages.value = ''
})

// Add a new task and emit it to TaskList
const addTask = () => {
  if (!name.value.trim()) {
    errorMessages.value = 'Task name is required'
    return
  }

  const newTask = {
    id: Date.now(),
    title: name.value,
    time: time.value || 'No time specified',
    done: false,
    editing: false,
  }

  emits('add-task', newTask) // Emit the task to TaskList
  emits('update:isAddTaskVisible', false) // Close the modal
  name.value = ''
  time.value = ''
}
</script>

<template>
  <v-dialog
    :model-value="isAddTaskVisible"
    @update:model-value="$emit('update:isAddTaskVisible', $event)"
    persistent
  >
    <v-row justify="center">
      <v-col cols="12" lg="6" md="8" sm="10">
        <v-card>
          <v-card-title class="text-center">Add Task</v-card-title>
          <v-card-text>
            <v-text-field
              v-model="name"
              :error-messages="errorMessages"
              label="Task Name"
              placeholder="Enter task name"
              required
            ></v-text-field>
            <v-text-field
              v-model="time"
              label="Time"
              placeholder="Enter time (optional)"
              suffix="PHT"
              type="time"
            ></v-text-field>
          </v-card-text>
          <v-divider></v-divider>
          <v-card-actions>
            <v-btn variant="text" @click="$emit('update:isAddTaskVisible', false)"> Cancel </v-btn>
            <v-spacer></v-spacer>
            <v-btn color="primary" @click="addTask">Submit</v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </v-dialog>
</template>
