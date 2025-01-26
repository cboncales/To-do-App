<script setup>
const listContainer = document.getElementById('list-container')
const inputBox = document.getElementById('input-box')
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
                onclick="addTask()"
              ></v-btn>
            </div>
            <v-card-text>
              <v-list>
                <v-list-item-group>
                  <v-list-item v-for="task in tasks" :key="task.id">
                    <v-list-item-icon>
                      <v-icon>mdi-checkbox-blank-outline</v-icon>
                    </v-list-item-icon>
                    <v-list-item-content>
                      <v-list-item-title>{{ task.title }}</v-list-item-title>
                      <v-list-item-subtitle>{{ task.description }}</v-list-item-subtitle>
                    </v-list-item-content>
                  </v-list-item>
                </v-list-item-group>
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
                onclick="addTask()"
              ></v-btn>
            </div>
            <v-card-text>
              <v-list>
                <v-list-item-group>
                  <v-list-item v-for="task in tasks" :key="task.id">
                    <v-list-item-icon>
                      <v-icon>mdi-checkbox-blank-outline</v-icon>
                    </v-list-item-icon>
                    <v-list-item-content>
                      <v-list-item-title>{{ task.title }}</v-list-item-title>
                      <v-list-item-subtitle>{{ task.description }}</v-list-item-subtitle>
                    </v-list-item-content>
                  </v-list-item>
                </v-list-item-group>
              </v-list>
            </v-card-text>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </v-main>
</template>
<style scoped></style>
