<script setup>
import { ref } from 'vue'
import TaskModal from './layout/TaskModal.vue'
const listContainer = document.getElementById('list-container')
const inputBox = document.getElementById('input-box')

const isVisible = ref(false)
const addTask = ref()
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
                @click="
                  () => {
                    isVisible = true
                  }
                "
              ></v-btn>
            </div>
            <v-card-text>
              <v-list>
                <v-list-item>
                  <v-icon>mdi-checkbox-blank-outline</v-icon>
                  <v-list-item-title>Take a Bath</v-list-item-title>
                  <v-list-item-subtitle>maligo ko</v-list-item-subtitle>
                </v-list-item>
              </v-list>
            </v-card-text>

            <v-divider></v-divider>

            <div class="d-flex justify-space-between">
              <v-card-title class="my-2">Tomorrow's Tasks</v-card-title>
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
                <v-list-item>
                  <v-icon>mdi-checkbox-blank-outline</v-icon>
                  <v-list-item-title>Take a Bath</v-list-item-title>
                  <v-list-item-subtitle>maligo ko</v-list-item-subtitle>
                </v-list-item>
              </v-list>
            </v-card-text>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </v-main>
  <TaskModal v-model:isAddTaskVisible="isVisible"></TaskModal>
</template>
<style scoped></style>
