<script setup></script>
<template>
  <div class="card">
    <slot></slot>
  </div>
</template>
<style scoped>
.card {
  background-color: white;
  border-radius: 12px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  padding: 20px;
  margin-bottom: 20px;
  color: black;
}
</style>
