<script setup>
defineProps({
  skillName: String,
});
defineEmits(["choose"]);
</script>

<template>
  <li @click="$emit('choose')">
    {{ skillName }}
  </li>
</template>

<style scoped>
li {
  cursor: pointer;
  padding: 5px 0;
}
</style>
