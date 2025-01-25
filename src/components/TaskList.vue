<script setup></script>
<template>
  <v-main style="height: 250px" app>
    <v-container>
      <v-row>
        <v-col cols="12">
          <v-card>
            <v-card-title>Today's Tasks</v-card-title>
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

            <v-card-title>Tomorrow's Tasks</v-card-title>
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
