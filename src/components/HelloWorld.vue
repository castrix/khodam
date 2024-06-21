<script setup lang="ts">
defineProps<{ msg: string }>()

</script>

<template>
  <h1>{{ msg }}</h1>

  <code>
    <b>Tulis nama lalu tekan enter</b>
  </code>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
