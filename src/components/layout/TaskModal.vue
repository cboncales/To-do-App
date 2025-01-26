<script setup>
import { ref, computed, watch } from 'vue'

const props = defineProps({
  isAddTaskVisible: Boolean,
})

// Reactive state
const errorMessages = ref('')
const name = ref(null)
const time = ref(null)
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

// Methods
const addressCheck = () => {
  errorMessages.value = address.value && !name.value ? `Hey! I'm required` : ''
  return true
}

const resetForm = (refs) => {
  errorMessages.value = []
  formHasErrors.value = false

  Object.keys(form.value).forEach((f) => {
    refs[f]?.reset?.()
  })
}

const submit = (refs) => {
  formHasErrors.value = false

  Object.keys(form.value).forEach((f) => {
    if (!form.value[f]) {
      formHasErrors.value = true
    }
    refs[f]?.validate?.(true)
  })
}
</script>

<template>
  <v-dialog :model-value="isAddTaskVisible">
    <v-row justify="center">
      <v-col cols="12" lg="6" md="8" sm="10">
        <v-card ref="form">
          <v-card-text>
            <v-text-field
              ref="name"
              v-model="name"
              :error-messages="errorMessages"
              :rules="[() => !!name || 'This field is required']"
              label="Task Name"
              placeholder="Take a bath"
              required
            ></v-text-field>
            <v-text-field
              :error-messages="errorMessages"
              :rules="[() => !!time || 'This field is required']"
              label="Time"
              model-value="12:30:00"
              suffix="PHT"
              type="time"
            ></v-text-field>
          </v-card-text>
          <v-divider class="mt-12"></v-divider>
          <v-card-actions>
            <v-btn variant="text" @click="$emit('update:isAddTaskVisible', false)"> Cancel </v-btn>
            <v-spacer></v-spacer>
            <v-slide-x-reverse-transition>
              <v-tooltip v-if="formHasErrors" location="left">
                <template v-slot:activator="{ on, attrs }">
                  <v-btn class="my-0" icon v-bind="attrs" v-on="on" @click="resetForm">
                    <v-icon>mdi-refresh</v-icon>
                  </v-btn>
                </template>
                <span>Refresh form</span>
              </v-tooltip>
            </v-slide-x-reverse-transition>
            <v-btn color="primary" variant="text" @click="submit"> Submit </v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </v-dialog>
</template>
