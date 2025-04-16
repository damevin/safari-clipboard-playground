<script setup lang="ts">
import CopyIssue from './components/CopyIssue.vue';
</script>

<template>
  <div>
    <h1>Playground Clipboard Issue</h1>
  <CopyIssue></CopyIssue>
  </div>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
