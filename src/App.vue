<script setup>
import AppBar from './components/AppBar.vue'
import NavDrawer from './components/NavDrawer.vue'
import TaskList from './components/TaskList.vue'
</script>

<template>
  <v-app>
    <!-- App Bar -->
    <AppBar />

    <!-- Navigation Drawer -->
    <NavDrawer />

    <!-- Task List -->
    <TaskList />
  </v-app>
</template>

<style scoped></style>
