<script setup>
import { computed } from 'vue'
import { useTheme } from 'vuetify'

const theme = useTheme()

// Toggle theme between light and dark
function toggleTheme() {
  theme.global.name.value = theme.global.current.value.dark ? 'light' : 'dark'
}

// Computed property to dynamically set the icon
const themeIcon = computed(() =>
  theme.global.current.value.dark ? 'mdi-weather-sunny' : 'mdi-moon-waning-crescent',
)
</script>

<template>
  <v-app-bar :elevation="2" color="blue-darken-1" app>
    <v-app-bar-title>To-do List App</v-app-bar-title>
    <v-btn icon @click="toggleTheme">
      <v-icon size="small">{{ themeIcon }}</v-icon>
    </v-btn>
  </v-app-bar>
</template>

<style scoped></style>
