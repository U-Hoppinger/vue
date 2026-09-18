<script setup>
import { ref } from "vue";
const myText = ref("learn");
const changeText = () => {
  if (myText.value === "learn") {
    myText.value = "New text";
  } else {
    myText.value = "learn";
  }
};
const isVisible = ref(true);
</script>

<template>
  <p>{{ myText }}</p>
  <button @click="changeText">Click me!</button>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
